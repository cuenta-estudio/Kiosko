| PROCESO | Análisis y Troubleshooting - Precios Kiosko |
|--|--|
|  AUTOR| @<17962A48-91CA-6013-93A7-25B88797E017>  |


[[_TOC_]]

----

## **Objetivo** 
:dart: El objetivo de esta guía es entregar visibilidad sobre algunos puntos claves a considerar cuando se presenten problemas en la carga de precios de Kiosko. Ya sea por un error desde el área de Unidad de Precios, por algún problema en el Worker y/o algún error directo en el archivo de carga de precios.

##**Información Base** 

:information_source: En Kiosko existen 3 Tipos de Precio:
- **Precio Normal:** Este precio nunca cambia, es el precio que se carga al SKU al momento de ser creado.
- **Precio Vigente:** Este precio es el que se carga todas las noches en el SFTP por el área de Negocio, el cual refiere aun precio "oferta", comparado con el Precio Normal.
- **Precio Promocional:** Este precio lo realiza el "motor de promociones", servicio que se aloja en el servidor de aplicaciones del Kiosko, el cual consume los precios de una API que administra el área de Negocios. Este precio será el precio promocional al comprar con la tarjeta de Abcdin.

 ###**Preguntas Frecuentes**

:question: **¿Cómo se realiza la carga de precios en Kiosko?**
Todas las noches, el área de Soporte Sistemas realiza una carga de precios en el SFTP de Kiosko. Esto mediante un archivo en formato TXT, el cual viene en el siguiente formato:

13303|10663|1126231|STUH03141126231|BAR DUKAT - W|BAR DUKAT - WENGUE |D|03|314|TUH|S|41464|20|13-JUN-19|04-JUN-19|18-JUN-19|72990
13303|10675|1121909|SCDL03101121909|SITIAL LONCOC|SITIAL LONCOCHE TERRA |V|03|996|CDL|S|56000|20|13-JUN-19|04-JUN-19|18-JUN-19|80990
13303|10675|1121910|SCDL03101121910|POLTRONA OSOR|POLTRONA OSORNO RESPALDO MADER|V|03|996|CDL|S|135500|20|13-JUN-19|04-JUN-19|18-JUN-19|195990
13303|10675|1121911|SCDL03101121911|POLTRONA OSOR|POLTRONA OSORNO RESPALDO TAPIZ|V|03|996|CDL|S|146500|20|13-JUN-19|04-JUN-19|18-JUN-19|210990
13303|10675|1121912|SCDL03101121912|POLTRONA LLAN|POLTRONA LLANQUIHUE BEIGE |V|03|996|CDL|S|173200|20|13-JUN-19|04-JUN-19|18-JUN-19|249990

Desde el cual, podemos distinguir los siguientes campos importantes:
**|10663|:** Aquí viene definido el número de la sucursal. Siempre vendrá un 10 por defecto, los últimos 3 dígitos será el número de sucursal. En este caso, sería la sucursal 663.

**|1126231|:** En este campo viene definido el SKU.

**|13-JUN-19|04-JUN-19|18-JUN-19|:** Estos dos campos de fecha definen la vigencia del precio, esto quiere decir (en este mismo orden): Fecha Inicio - Fecha Fin.

**|72990|:** este último campo, tiene el precio del producto.

El formato del nombre del archivo de carga es el siguiente:
![image.png](/.attachments/image-fbdc1f2e-39d9-4659-af7c-787cd5cca475.png)

Este formato se debe mantener siempre, de lo contrario puede que el Worker no identifique la carga.
Los datos dentro del archivo de carga siempre deben venir en este formato y es de exclusiva importancia que la primera línea contenga los datos seleccionados a continuación.
![image.png](/.attachments/image-c8087884-eb8a-40ec-bb17-09eda22b7673.png)

```
"id_batch_prc|cod_sucursal|cod_producto|cod_largo_producto|desc_corta_producto|desc_larga_producto|estado_producto|linea|familia|marca|tipo_producto|costo_promedio|tipo_prec
io|fecha_transmision|fecha_inicio|fecha_termino|precio"
```

:question: **¿Por qué necesitamos esta data?**
Porque la carga de precios en Kiosko involucra valores diferentes para cada tienda. Esto quiere decir que puede existir diferencia de precios de un mismo SKU, entre una Sucursal y otra.

:question: **¿Qué es y/o qué hace el Worker?**
El Worker es un servicio desplegado en nodejs que que realiza tareas, por ello el nombre como tal "Worker".
En este caso, el Worker realiza un proceso diario y durante la madrugada, el cual detecta que exista algún nuevo archivo (con el formato correcto) en el SFTP de carga de precios (Administrado por TI). Una vez que este archivo ha sido detectado, este proceso toma el mismo y lo procesa para insertar toda la información correspondiente al Kiosko, en la base de datos. 


----
### **Casuistica** 

:information_source: Cuando reportan problemas de precios en Kiosko o necesitan validar que estos se hayan cargado correctamente, existe una serie de pasos base que podemos seguir.
- Revisión vía SFTP del archivo correspondiente a la carga de precios proveniente desde Unidad de Precios.
- Revisión de archivos procesados en API filelogs.
- Revisión de precios en por Base de Datos.
- Revisión del servicio del Worker.

----
### **Check list accesos** 
:white_check_mark: Para esta revisión necesitaremos lo siguiente:
- [X] Para la vista de la API se recomienda Firefox o en Chrome: Descargar Extensión JsonView.
- [X] Accesos al SFTP de Kiosko:
```
Hostname: 200.54.96.56
Username: Kiosko
Password: UJmnb2q.,
Puerto: 22
Path Files: /home/Kiosko/procesados/
```
- [X] Acceso a Base de Datos Kiosko y Servidor Worker. Para esto revisar Check List - Accesos Nivel 1.
----
###Datos a Solicitar
Debemos tener claro qué datos debemos solicitar para realizar una primera revisión. 

:information_source: Necesitaremos al menos 1 SKU (de preferencia el SKU con problemas), el número de la Sucursal y el valor que debería tener el SKU en esa Tienda.

----
##Procedimiento
En una primera instancia, validaremos que el archivo de carga de precios haya sido cargado en el SFTP.
- Nos aseguraremos de estar en el directorio indicado: /home/Kiosko/procesados/
- Nos fijamos en el nombre del archivo y la fecha de modificación de este. Esto nos quiere decir la fecha y hora en la que fueron cargadoslos precios.

![image.png](/.attachments/image-5c1db310-f328-4585-b077-a77a3f4049f2.png)

Ahora con esta data, validaremos en la API, que este archivo haya sido procesado.

https://app.abcdin.cl/api/filelogs

Validamos que el archivo que se cargó en el SFTP se encuentre en estado "procesado". Esto quiere decir que fue correctamente consumido por
el Worker.
![image.png](/.attachments/image-cfdc4a84-217c-4629-86cb-5715099cf270.png)

Al validar estos 2 pasos, se entiende que la carga de precios se realizó correctamente y fue procesado en las bases de datos.

El siguiente paso será validar el SKU en la tienda correspondiente, validar el precio en el archivo cargado y validar que sea consistente con la base de datos.

Para este caso, tomaremos como ejemplo el SKU 1126318 en la Sucursar 682.
_Nota: Se recomienda descargar localmente el archivo de carga de precios, para poder revisar sin problemas._

Buscando el SKU y Sucursal, encontramos que el precio corresponde a 80990.
![image.png](/.attachments/image-c643d574-2a94-4875-bdcc-1f6aab2d5ea6.png)

Ahora revisaremos en la Base de Datos, con la siguiente Query, En donde shop_code será el número de la Sucursal; sku será el código del Producto.

`select * from product_prices inner join product_promotions on
product_prices.id=product_promotions.product_price_id where
shop_code=10682 and sku='1126318';`

Esto nos dará el siguiente resultado en la BD, en donde podremos validar el precio, la fecha que se realizó el insert en la base, el número de
SKU y los demás datos asociados.
![image.png](/.attachments/image-d9942cb6-3131-4a3e-9eff-d18d4e5ba929.png)

Hasta aquí hemos validado que se encuentra todo bien, realizando el flujo de la carga de precios.

En el caso en que vemos una inconsistencia entre el archivo de carga de precios y la base de datos, o en la API vemos que el archivo no fue procesado, es posible que sea necesario el reinicio del servicio del Worker.
**En este paso, se recomienda primero contar con la validación del Nivel 2.**

En el servidor del Worker, **con el usuario ubuntu**: Realizando el siguiente comando, podemos validar que el servicio se encuentra arriba.

`#pm2 list`
![image.png](/.attachments/image-61cafdd8-af93-4bbc-b778-1996113c223b.png)

Los siguientes comandos para reiniciar el servicio serán:

```
#pm2 restart 'abcdin-price-worker'
```
Luego de esto, validaremos que el servicio se encuentre nuevamente arriba, con el comando `#pm2 list.`

Los siguientes pasos luego de esto, serían revisar nuevamente que el archivo de carga haya sido procesado y que la data sea consistente en la bases de datos.

