Historia: 
#233

| Descripción | Venta de combos en kiosko |
|--|--|
[[_TOC_]]

----
#Compendio Técnico

A continuación se informan los cambios realizados a nivel de Desarrollo.

----

##Contexto
_Desarrollo que contempla la búsqueda y posterior venta de combos disponibles en la página web de la tienda desde el kiosko._ 

----

##Desarrollo
###Vista de combos
**FrontEnd:**
1. Se intervienen los siguientes archivos:
   - /src/components/productView/ProductView.scss

2. Esto permite mostrar en la vista de resultados de búsqueda no solo si un producto se encuentra disponible, también lo muestra como artículo componente de un combo.

###Procesamiento de combos
**Backend**
1. Se crea nuevo componente llamado **_orderProductCombos_** con su respectivo controlador.
2. Este controlador contiene métodos que permiten el procesamiento de la información para poder realizar de forma correcta una venta. Algunos de los métodos son:
   - getComboPricesForCatalog
   - getCombosFromCatalog
   - getComboPricesFromIbm
   - joinCatalogWithCombos
   - buildCombosForCatalog

3. El componente orderProductCombos interactúa con los siguientes archivos, los cuales fueron modificados:
   - /src/components/order/controller.js
   - /src/components/orderProductsWarranties/controller.js
   - /src/components/orderShippingAccount/controller.js
   - /src/components/orquestador/confirmStock.js
   - /src/components/orquestador/index.js
   - /src/components/orquestador/ticket.js
   - /src/components/product/controller.js
   - /src/components/orquestador/index.js
   - /src/middlewares/tlog/formatTlogJson.js


###Funcionalidad
A continuación se entrega información relevante de acuerdo a la funcionalidad del desarrollo.

1. La aplicación kiosko originalmente trabaja con un caché de información el cual está configurado con uan duración de 60 minutos, para este desarrollo, esa duración fue disminuida a 30 minutos con el objetivo de tener mayor sincronización con la mantención realizada a los combos en el commerce.

2. A nivel de frontend, el desarrollo no solo muestra los combos provenientes de abcdin.cl, permite realizar una búsqueda por cualquier producto y si este es parte de un combo, también lo muestra como resultado.

3. Venta-Combos omite el proceso de despublicación de productos por manejo de stock, esto por ser productos no mantenidos por la tienda.

4. A nivel de backend, el desarrollo se comporta de la siguiente manera:
   - Al igual que el desarrollo original, el frontend consulta al endpoint /products/search/catalog/:searchTerm?pageSize=50&pageNumber=1 pasándole el termino que se buscó.
   - Esta URL consulta al servicio wcs (Catálogo IBM), por medio de la variable de entorno ENDPOINT_WCS.

----
#Documentación Operaciones
_A continuación se entregará información relevante de acuerdo a las modificaciones realizadas, correspondiente a la Operación y cómo Operar los nuevos cambios en producción. Vale decir: Diagramas de flujo asociados en caso de aplicar, validaciones a realizar, tips de revisión y pruebas funcionales._

##QA 



Se agregaron combos en el kiosco y estos se ven de la siguiente manera en PLP:

![PLP de combo .png](/.attachments/PLP%20de%20combo%20-c15e493f-0b6e-4727-bd96-a91b4d1f1a0b.png)

El PDP del combo de la siguiente manera

![combo PDP.png](/.attachments/combo%20PDP-dca90781-2497-40d1-b081-f6a4c046e77b.png)


El Tlog que se puede ver desde la siguiente ruta: kioskopriv-qa  /648/20/2020-06-05/ (dentro de esta ruta llegan todas las boletas y los Tlog de Kiosco QA) y se muestran correctamente de la siguiente manera 

![boleta.png](/.attachments/boleta-4f3ed384-0ecd-4539-818c-e05b4551e1f0.png)

![tlog.png](/.attachments/tlog-c77ff412-4839-4a22-8239-9df31087be4f.png)

Los combos en Kiosco poseen los mismos precios que en el Ecommerce 

![mismo precio kiosco.png](/.attachments/mismo%20precio%20kiosco-d4bdeb12-ac9c-462e-8ed7-0e5de06b6612.png)

![mismo precio ecommers.png](/.attachments/mismo%20precio%20ecommers-4e5b096a-3c05-4d6d-b944-d928e111cd55.png)