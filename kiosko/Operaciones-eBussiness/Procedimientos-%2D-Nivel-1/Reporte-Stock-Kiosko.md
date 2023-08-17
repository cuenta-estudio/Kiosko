
| PROCESO | Mitigación Productos Ret Tienda publicados en Catalogo con Stock 0 |
|--|--|
|  AUTOR| @<17962A48-91CA-6013-93A7-25B88797E017>  |
| BUG | #1256 |

[[_TOC_]]

----

### **Objetivo** :dart:
El objetivo de este procedimiento mitigar los productos del eCommerce que son Retiro en Tienda, cuentan con stock 0 para despacho a Domicilio y se encuentran Disponibles en el Catálogo del Kiosko.
### **Mitigación** 
De Cara a Operaciones lo que se realiza técnicamente es enviar todos los productos que cuenten con este síntoma a una "Blacklist", lista negra que se encuentra en la base de datos del Kiosko, la cual despublica cualquier producto que se encuentre en esa Tabla.

**check list accesos* :white_check_mark:

- [X] validar conexión BD eCommerce
- [X] validar conexión BD Kiosko
- [X] validar conexión Servidor de Aplicación Kiosko

----
## Reporte Stock Kiosko

**Información**
Se genera un reporte AM considerando el siguiente template [Reporte Stock Kiosko.xlsx](/.attachments/Reporte%20Stock%20Kiosko-fd281917-6e64-4776-95d3-26949e672e06.xlsx), el cual considerará los siguientes pasos.

----

## Procedimiento
Ya con el template abierto, comenzamos generando la siguiente Query de Consulta en la base de datos eCommerce/LIVE:


_-------#Reporte Stock Kiosko#-LIVE
SELECT CAT.PARTNUMBER AS "SKU", CATDESC.NAME, inv.QUANTITY AS "STOCK",inv.FFMCENTER_ID AS "TIENDA", 
CATDESC.PUBLISHED AS "PUBLICADO",CAT.BUYABLE AS "COMPRABLE",CAT.MARKFORDELETE AS "HABILITADO",AVD.VALUE AS "RET TIENDA" 
FROM WCSDB.CATENTDESC CATDESC 
INNER JOIN WCSDB.CATENTRY CAT ON CAT.CATENTRY_ID = CATDESC.CATENTRY_ID 
LEFT JOIN WCSDB.inventory INV ON INV.catentry_ID = CATDESC.catentry_ID 
INNER JOIN WCSDB.CATENTRYATTR CATT ON CATT.CATENTRY_ID = CAT.CATENTRY_ID 
INNER JOIN WCSDB.ATTR AR ON AR.ATTR_ID=CATT.ATTR_ID 
INNER JOIN WCSDB.ATTRVAL AV ON AV.ATTRVAL_ID = CATT.ATTRVAL_ID 
INNER JOIN WCSDB.ATTRVALDESC AVD ON AV.ATTRVAL_ID = AVD.ATTRVAL_ID 
WHERE  1=1 
AND INV.FFMCENTER_ID IN ('10001') 
AND CAT.BUYABLE = 1 AND CATDESC.PUBLISHED = 1 
AND CAT.MARKFORDELETE = 0 AND INV.QUANTITY = 0 
AND AR.IDENTIFIER LIKE ('%RetTienda%') AND AVD.VALUE = 'YES' 
WITH UR;_

Lo que realiza esta consulta es validar todos los productos del eCommerce que tengan el atributo Retiro en Tienda en "YES" y cuenten con stock 0 para despacho a domicilio (FFMCENTER_ID = 10001).

Una vez tengamos los resultados de la Query, se exportará el csv, se ordenarán en Columnas y se copia toda la información a la pestaña "Reporte eC" del template.
![image.png](/.attachments/image-7e82b5df-6135-4913-ae58-476ef7872ce4.png)

Ahora realizamos la siguiente consulta en la base de datos de Kiosko:

_SELECT sku AS "SKU", app_scope AS "blacklist",created_at AS "Fecha Creación"
FROM forbidden_products ;_

Exportaremos esta información, la ordenaremos en columnas y copiaremos la información completa en la pestaña "Reporte BL".
![image.png](/.attachments/image-aa13af8c-1473-4fb8-9361-689138803ac5.png)

Luego Copiamos el listado completo de la Columna "SKU" en la pestaña "Reporte eC" y la pegamos en la pestaña "Valida BL".
Nota: La segunda columna de esta pestaña contiene fórmulas, por lo tanto solo debemos reemplazar el SKU.
![image.png](/.attachments/image-a346be3f-f04f-43eb-865e-87d2277f749a.png)

Ahora seleccionamos las celdas B y C de la columna 2 y haremos doble click en la esquina de la celda C3 ó arrastramos hacia abajo, hasta el último producto en la lista. Esto copiará el formato de las fórmulas para cada columna hacia abajo.
![image.png](/.attachments/image-06fe05bf-51bc-45a7-971d-ebf16e3168a2.png)

Ahora Ordenaremos los productos de la pestaña "Reporte BL" para copiarlos en la siguiente Query, la cual ejecutaremos nuevamente en la Base de Datos del eCommerce/LIVE:

_--#Segunda Query_Validación Stock-LIVE
SELECT CAT.PARTNUMBER AS "SKU", CATDESC.NAME, inv.QUANTITY AS "STOCK",inv.FFMCENTER_ID AS "TIENDA", 
CATDESC.PUBLISHED AS "PUBLICADO",CAT.BUYABLE AS "COMPRABLE",CAT.MARKFORDELETE AS "HABILITADO",AVD.VALUE AS "RET TIENDA" 
FROM WCSDB.CATENTDESC CATDESC 
INNER JOIN WCSDB.CATENTRY CAT ON CAT.CATENTRY_ID = CATDESC.CATENTRY_ID 
LEFT JOIN WCSDB.inventory INV ON INV.catentry_ID = CATDESC.catentry_ID 
INNER JOIN WCSDB.CATENTRYATTR CATT ON CATT.CATENTRY_ID = CAT.CATENTRY_ID 
INNER JOIN WCSDB.ATTR AR ON AR.ATTR_ID=CATT.ATTR_ID 
INNER JOIN WCSDB.ATTRVAL AV ON AV.ATTRVAL_ID = CATT.ATTRVAL_ID 
INNER JOIN WCSDB.ATTRVALDESC AVD ON AV.ATTRVAL_ID = AVD.ATTRVAL_ID 
WHERE 1=1 
AND INV.FFMCENTER_ID IN ('10001') 
AND AR.IDENTIFIER LIKE ('%RetTienda%') 
AND AVD.VALUE = 'YES' 
AND CAT.PARTNUMBER IN (AQUÍ INGRESA LOS SKUs) 
WITH UR;_
![image.png](/.attachments/image-c872fac9-f031-4d2f-bcb1-2296dee6eeb9.png)

Exportaremos esta información y la copiaremos en la pestaña "Stock BL eC" *Considerando las columnas A-H*.
![image.png](/.attachments/image-0002f1ec-fa8c-42aa-92c2-e818b2a7fa90.png)


Arrastraremos la fórmula de la celda I2 hacia abajo para hacer efectiva la fórmula en la columna completa.
![image.png](/.attachments/image-9d03e2f9-72eb-4776-baa7-4cf6f0b2ea3e.png)

----
## Tablas Dinámicas

Ahora iremos a la pestaña "Informe", para realizar el cuadre de toda esta información que hemos recopilado.

Hacemos click en la tábla dinámica "Productos en eCommerce a Despublicar" y ajustaremos lo datos a considerar en la tabla.
![image.png](/.attachments/image-3953ccd3-fcc5-4b8e-97ee-dd32ac5a643f.png)

Seleccionaremos la tabla completa que necesitamos:
![image.png](/.attachments/image-7e193004-24eb-420c-a332-cfe24707e11c.png)

_Nota: En caso que la información no actualice, podremos actualizar con la siguiente opción:_
![image.png](/.attachments/image-33b9abbd-bfec-40e8-9c6d-92d8ed65793c.png)

Al realizar estos 2 pasos la tabla se actualizará y mostrará los productos a considerar.
![image.png](/.attachments/image-7411dbef-3697-4670-a6e0-fe5b2eeb5aa0.png)

Realizaremos lo mismo con las 2 tablas.
![image.png](/.attachments/image-dd5da334-d576-41f0-b25b-75b10afe22fc.png)

----
## Publicar/Despublicar Productos

**Blacklist Kiosko**

Ya con las tablas dinámicas consolidadas, procedemos a mitigar.

**Productos en eCommerce a Despublicar**
Consideraremos todos los productos que se encuentren bajo la celda "AGREGAR BL" y los agregaremos a la lista negra de Kiosko.
![image.png](/.attachments/image-c73d97ce-f378-468c-a3a9-70da657b56fc.png)

Copiaremos estos productos, los pegaremos en la pestaña "Ops" desde la celda A3 y arrastraremos la celda B3 para que la fórmula aplique al resto de la columna.
![image.png](/.attachments/image-3d65186f-81da-4361-8503-f221b85417ac.png)

:warning:Importante:warning: 
Fijarse en quitar la "coma" del último producto en la lista.
![image.png](/.attachments/image-8fed6255-9d5a-4411-957f-9b76f01dc38d.png)

Ya con los productos en formato, nos conectaremos al servidor de aplicación en el cual ocuparemos el siguiente comando:

`curl --header "Content-Type: application/json" --request POST --data '[ "SKU" ]' http://localhost:4000/products/forbiddenProducts
`

El cual, ingresando los productos, quedará de la siguiente manera:

`curl --header "Content-Type: application/json" --request POST --data '[
{"sku": 1109965},
{"sku": 1122439},
{"sku": 1131819},
{"sku": 1127983},
{"sku": 1136017},
{"sku": 1135814},
{"sku": 1137200}
]' http://localhost:4000/products/forbiddenProducts
`


Ejecutaremos el comando en el App Server. En donde confirmaremos la ejecución del comando con el siguiente mensaje de respuesta:
![image.png](/.attachments/image-3fa120db-e870-45d7-bcd6-f2b749bc0d94.png)

**Productos en eCommerce a Despublicar**
En esta tabla dinámica consideraremos todos los productos que aparezcan en la tabla "A PUBLICAR".
![image.png](/.attachments/image-2840ff67-2206-4010-8d03-a9abf5cabaf1.png)

Quitaremos estos productos de la lista negra porque ya tienen nuevamente stock. Realizaremos esta tarea con el siguiente comando

`curl --header "Content-Type: application/json" --request DELETE --data '[ "SKU" ]' http://localhost:4000/products/forbiddenProducts
`
Realizaremos el mismo procedimiento en la pestaña "Ops" de la plantilla para obtener el formato de los SKU's y luego de copiados en el comando, la instrucción quedará de la siguiente manera:

`curl --header "Content-Type: application/json" --request DELETE --data '[
{"sku": 1142421},
{"sku": 1142114},
{"sku": 1137184},
{"sku": 1142230},
...
...
{"sku": 1117697},
{"sku": 846602},
{"sku": 1119754}
]' http://localhost:4000/products/forbiddenProducts
`
Luego de ejecutado el comando, confirmaremos con el siguiente mensaje del servidor de aplicación:
![image.png](/.attachments/image-9072c3de-fed7-443a-9907-7aae03c831d8.png)

**Validación Nuevos Productos en Blacklist**

Si queremos realizar una validación adicional sobre estos productos en lista negra, podemos realizar la misma query utilizada en un principio en la base de datos de Kiosko:

_SELECT sku AS "SKU", app_scope AS "blacklist",created_at AS "Fecha Creación"
FROM forbidden_products ;_

Con esto hemos terminado la mitigación como tal, el resto corresponde a generar la comunicación vía correo a los Stakeholders correspondientes.
![image.png](/.attachments/image-07f0c3bc-8c2b-42c6-b57f-dde6a7799ef5.png)