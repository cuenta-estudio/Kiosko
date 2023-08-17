#14084
[[_TOC_]]

---
# Compendio Técnico
A continuación se informan los cambios realizados a nivel de Desarrollo.

---
## Contexto
Se requiere revisar el stock de productos en 2 instancias del proceso:
1. En el catálogo de productos, al momento de *agregar* un producto al carro de compras.
2. En la ficha del producto, al momento de presionar *comprar*.

En caso de no existir stock del producto, este debe ser despublicado.
Adicionalmente la despublicación debe realizarse al momento de finalizar una compra, en donde se haya consumido todo el stock del producto.

---
## Desarrollo

### BackEnd

Se crean dos nuevos endpoints, bajo el componente *products*:
1. **_/products/stockBySku/:sku_** Dado un sku, utiliza la función ya existente "stockByProduct", para obtener si existe o no stock del producto. En caso de no existir producto, este es almacenado en una tabla en _redis_ con la siguiente nomenclatura "fecha-idSucursal", donde fecha se encuentra en formato AAAA-MM-DD.
2. **_/products/unpublishMaterials_** Este endpoint recibe, en el body, un arreglo el cual contiene una lista de productos los cuales serán insertados en la tabla mencionada en el punto anterior.

Se modifica función **_getBySearchTerm_**, a la cual se le agrega lógica que una vez recibidos los resultados de la búsqueda, revise si estos se encuentra o no en la tabla del punto 1 [anterior], y en caso que exista el valor, este es marcado como "no disponible"

### FrontEnd

Se intervienen las siguientes funciones/componentes:
1. Componente _ProductView_, función _getWarranties_, en donde se le agrega lógica, para consultar stock del producto, previo a consulta de garantia. En caso que el producto tenga stock continua normalmente, en caso contrario se despliega mensaje de error de stock
2. Componente _Product_, funcion _onAddToCartClick_, Cambio análogo al anterior.


---

#Documentación Operaciones
_A continuación se entregará información relevante de acuerdo a las modificaciones realizadas, correspondiente a la Operación y cómo Operar los nuevos cambios en producción. Vale decir: Diagramas de flujo asociados en caso de aplicar, validaciones a realizar, tips de revisión y pruebas funcionales._

##QA 

-Cuando se consulta el stock desde botón añadir y producto no cuenta con stock este debe de enviar un mensaje comentando que el producto no cuenta con stock y des publicar el mismo y se visualiza de esta manera
  

![image.png](/.attachments/image-19841719-b9aa-477a-ac49-e6fe416c4840.png)![Screenshot-2020-12-18T20-07-20.728Z.png](/.attachments/Screenshot-2020-12-18T20-07-20.728Z-39a42d46-ae9b-4956-b16a-3827ef30f55f.png)




-Cuando se consulta stock desde botón comprar y producto no cuenta con stock este debe de enviar un mensaje comentando que el producto no cuenta con stock y des publicar el mismo y se visualiza de esta manera

![image.png](/.attachments/image-c1044f63-abbf-4443-9ab2-d680166110ac.png) 

![image.png](/.attachments/image-e1ab34f8-23ca-467b-a2a9-58e67f563be3.png)



-Cuando se realiza la consulta de stock y el stock no tiene la cantidad solicitada en este caso se envía un mensaje comentando cuanto tiene de stock disponible y descuenta del carrito de compra dejando el stock disponible y se visualiza de esta manera

![Screenshot-2020-12-21T14-04-17.461Z.png](/.attachments/Screenshot-2020-12-21T14-04-17.461Z-af57953e-da62-4983-8567-c858801313b0.png)

![image.png](/.attachments/image-e501730b-a048-42a2-9022-b288a00b1704.png)
  

-Cuando se realiza una compra y la misma agota el stock del producto este debe de desplubicar luego de agotar su stock y se visualiza de esta manera 
 
![Screenshot-2020-12-21T14-35-27.624Z.png](/.attachments/Screenshot-2020-12-21T14-35-27.624Z-303385e7-01ad-42ab-b9e2-3b34401098c4.png)
