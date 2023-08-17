| PROCESO | Actualización - Carga de precios |
|--|--|
|  AUTOR| @<17962A48-91CA-6013-93A7-25B88797E017>  |


[[_TOC_]]

----

## **Objetivo** 
:dart: El objetivo de este procedimiento es detallar las tareas a realizar cuando se presenten problemas en la carga de precios de Kiosko. Ya sea por un error desde el área de Unidad de Precios, o por algún problema en el Worker y/o algún error directo en el archivo de carga de precios.

----
**Info** 

:information_source: Existen 2 maneras de modificar precios en Kiosko:

**Actualización de Precios desde los Servidores de Aplicación:** Se realiza un "Update" en los productos involucrados para TODOS los Kioskos, por lo tanto no discrimina precios por tienda.
**Carga de Precios via SFTP:** Este procedimiento gatilla una carga de precios desde el Worker y dado el formato que requiere, esta carga considera precios para productos por tienda, a diferencia de la actualización de precios.

Para el caso de ambos procedimientos, la información inicial siempre debe venir desde el equipo de Unidad de Precios o también podría llegar desde Sistemas, Raul Díaz.

_Nota: Debemos ser rigurosos con esta información. Si no nos envían el template o archivo de carga y de manera correcta, **NO** debemos ejecutar nada._ 

----
##Actualización de Precios

###Considerar previo a Actualización
Para realizar este procedimiento, el negocio nos debe enviar este formulario completado:
[Template_CargaPreciosKiosko.xlsx](/.attachments/Template_CargaPreciosKiosko-604edeb6-d8b4-47a9-acd0-5d47ad2ffb6f.xlsx)

El template consta de los siguientes campos:
- **SKU:** Código del Producto
- **Date from – to:** Vigencia que tendrá el precio.
- **Price:** El precio que tendrá el producto.

![image.png](/.attachments/image-4ebc4a07-00ed-4e0d-a958-5d4a721888b0.png)

Así mismo, el template contiene 2 pestañas:
- **Pestaña _"Precios"_:** Vendrá con los datos cargados por parte del área de Negocios.
- **Pestaña _"No editar"_:** Utilizaremos esta pestaña para el procedimiento. Esta se encuentran protegida por contraseña: passw0rd

![image.png](/.attachments/image-9996df5c-beca-47e9-a038-9c6f8b9bacc9.png)

----
###Procedimiento Actualización de Precios
Una vez recibida esta planilla, desbloqueamos la pestaña "No editar" y veremos que los datos almacenados por el área de Negocio se encuentran concatenados en el siguiente formato:
 
![image.png](/.attachments/image-4ba5fe4f-9f4b-4af2-afcc-1be134f02a1b.png)

La concatenación será utilizada dentro del siguiente comando, el cual debemos ejecutar en cualquiera de los 2 servidores de aplicación de Kiosko:

`curl --header "Content-Type: application/json" --request POST --data '[]' http://localhost:4000/prices/productPromotions
`

Copiaremos tantas columnas sean necesarias, según precios solicitados.
![image.png](/.attachments/image-e59ff784-5087-4b05-989f-8426ba6f54ea.png)

Pegaremos esta data entre los campos [] del comando mencionado, lo cual debería quedar de la siguiente manera:

`curl --header "Content-Type: application/json" --request POST --data '[{"sku": "1126642","date_from": "04/03/2019","date_to": "04/03/2019","price": "129493"}]' http://localhost:4000/prices/productPromotions
`
_Nota: Tener en cuenta la "coma" al final de esta concatenación, la cual debe eliminarse en la última línea a cargar._

Se ejecutará este comando en el App1 Server y comenzará a procesar la data. Al procesar sin problemas aparecerá este mensaje:

`{"message":"All prices succesfully inserted"}`

----
##Carga de Precios

:information_source: Para realizar este procedimiento se requiere crear conexión al servidor SFTP de Kiosko.

Credenciales para acceso vía SSH y/o SFTP:
HOST=200.54.96.56 
PORT=22 
USER=Kiosko 
PASSWD=UJmnb2q.,
ruta de carga de archivos: /home/Kiosko/procesados

###Considerar previo a Carga
- El formato del nombre del archivo de carga es el siguiente:
![image.png](/.attachments/image-fbdc1f2e-39d9-4659-af7c-787cd5cca475.png)

Este formato se debe mantener siempre, de lo contrario puede que el Worker no identifique la carga.
- Los datos dentro del archivo de carga siempre deben venir en este formato y es de exclusiva importancia que la primera línea contenga los datos seleccionados a continuación.
![image.png](/.attachments/image-c8087884-eb8a-40ec-bb17-09eda22b7673.png)

```
"id_batch_prc|cod_sucursal|cod_producto|cod_largo_producto|desc_corta_producto|desc_larga_producto|estado_producto|linea|familia|marca|tipo_producto|costo_promedio|tipo_prec
io|fecha_transmision|fecha_inicio|fecha_termino|precio"
```
- En el caso que la carga considere una cantidad muy grande de registros, podría llegar a fallar y en este caso sería necesario dividir el archivo inicial en partes. **Es de vital importancia que cada archivo que se genere, tenga la primera tenga el formato mencionado en la imagen anterior.**

----
:warning:**Importante**:warning:
**El Worker Realiza la carga de precios al minuto 00 de cada hora, por lo tanto es necesario considerar siempre el horario previo a la carga.** 
**Es posible cargar más de un archivo simultáneamente al SFTP. Sin embargo, no los cargará todos al mismo tiempo, siempre considerará el nombre del archivo en orden de Fecha y Hora.**

----

###Procedimiento Carga de Precios
Es importante que dentro de el archivo de carga, se encuentre la tienda que requiere los cambios o carga de precios. Por ejemplo si la carga de precios va para la tienda 280, siempre en el archivo de carga irá el número de la tienda con un 10 previo, como correlativo.
![image.png](/.attachments/image-361e928e-f5bc-4414-ba87-39ff936e0cff.png)

Antes de cargar el archivo al directorio SFTP, se recomienda tomar en cuenta los archivos que ya han sido cargados en el directorio.
Es muy probable que Negocios nos envíe el archivo con un nombre similar a este: CI_KIOSKO_20200206_1211.
En caso de ser así o si es que tiene cualquier otro nombre, debemos validar que la información que contiene este archivo sea el correcto, luego de esto solo debemos cambiar el nombre al formato necesario.

![image.png](/.attachments/image-67790811-3fe6-4e52-a6e8-47eb4a8dc1fd.png)

Y según estos archivos, SIEMPRE CONSIDERAR LA FECHA, los correlativos previos y posteriores pueden cambiar. Por ejemplo, considerando la imagen anterior, el nombre podría ser el siguiente:
![image.png](/.attachments/image-7365fa4d-902f-454e-b63f-736822802d53.png)

En caso de agregar más de un archivo, simplemente fijarse que las horas de carga vayan en orden, considerando el siguiente ejemplo:
![image.png](/.attachments/image-1986e96f-d9ee-4e98-95b1-4f4031485b00.png)

Al realizar esto, la carga de precios ha sido realizada. Solo debemos esperar que el Worker detecte los archivos y los vaya procesando.

----

##Validación de Actualización/Carga de Precios
Al realizar la actualización de precios, la primera validación es el siguiente mensaje:
![image.png](/.attachments/image-ba738f70-a2a2-4048-a59a-1078e049794b.png)

La otra manera de validar es directo en la base de datos de Kiosko, ejecutando la siguiente Query:
_En donde "shop_code" es el ID de la tienda y "sku" es cualquier producto a validar._

_select PO.file_log_id, PP.product_price_id, PO.shop_code as "Tienda", PO.sku as "SKU", PO.normal as "Precio Normal", PP.price as "Precio Vigente",
PP.date_from as "Fecha Inicio", PP.date_to as "Fecha Fin", PP.created_at as "Creacion Precio Vigente", PP.updated_at as "Update Precio Vigente"
from product_prices PO
inner join product_promotions PP on PO.id = PP.product_price_id 
where 1=1
--Busca por ID de Tienda--
and shop_code=10280
--Busca por SKU--
and sku='1132368' 
--Busca por Fecha--
--and PP.created_at = '2020-03-12'
--and PP.date_to = '2009-01-07';_

Con esta query podríamos validar la actualización del precio del producto.
![image.png](/.attachments/image-b9c1e408-98ad-4414-95e2-a75984965252.png)
_NOTA: Siempre el precio a validar es el Precio Vigente._

Al realizar la carga de precios directo al Worker, utilizaremos la siguiente URL para validar:  (Se recomienda https://app.abcdin.cl/api/filelogs Firefox, de otra manera sería necesario instalar una extensión al browser que permita leer un formato JSON).

En este endpoint podemos validar el archivo que ha sido procesado, la fecha y el estado.
![image.png](/.attachments/image-fd8942b8-fb53-4851-b625-743be1d11389.png)

Otra manera de validar que el archivo procesado es ejecutando la siguiente query en la base de Kiosko.
`select name as "Archivo", type as "Tipo Carga", creation_date as "Fecha Creación", state as "Estado" from files_logs ;
`
En caso que la carga tenga un problema, debería aparecer tanto en el endpoint, como en la base de datos el estado "error" o también puede que se haya quedado pegado en estado "processing" por mucho tiempo.

![image.png](/.attachments/image-ce3abfc4-e96f-434c-a290-3d0dca68f805.png)