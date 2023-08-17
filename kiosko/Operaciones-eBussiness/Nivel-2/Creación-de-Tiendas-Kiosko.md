| PROCESO | Creación de Tiendas Kiosko |
|--|--|
|  AUTOR| @<17962A48-91CA-6013-93A7-25B88797E017>  |


[[_TOC_]]

----

## **Objetivo** 
:dart: El objetivo de este procedimiento es entender los procesos involucrados para la creación de una tienda en Kiosko, así también para ejecutar la tarea de Habilitación de un Kiosko.

----
**Info** 

:information_source: A continuación se adjunta el siguiente diagrama de flujos, en el donde se visualiza cada parte involucrada durante la habilitación de un Kiosko.
[Workflow - Creación Tienda Kiosko.jpg](/.attachments/Workflow%20-%20Creación%20Tienda%20Kiosko-ec538180-37b3-4670-9460-814deb3693ef.jpg)
 ![Workflow - Creación Tienda Kiosko.jpg](/.attachments/Workflow%20-%20Creación%20Tienda%20Kiosko-1da31c27-98cb-4d08-8ccc-a8fa8ee8f495.jpg)
_Nota: Este flujo ha sido actualizado para lo que refiere la carga de precio, actividad que ahora la realiza sistemas mediante Francisco Candia._


Así también, se adjunta un documento, en el cual se especifica en detalle cada tarea.
[Procedimiento habilitación KIOSCO.PDF](/.attachments/Procedimiento%20habilitación%20KIOSCO-dccbf97d-f4ea-4901-a9ea-f892a2fff394.PDF)

----
##Habilitación Kiosko

La solicitud de habilitación de tienda viene desde el equipo de Soporte Sistemas mediante ticket, en el cual debe venir explicito los siguientes datos:
 
- Sucursal
- Nombre Tienda
- Ip 1
- Terminal_id
- Store_id
- bm_ip
- bm_url


Ejemplo:

```
Suc283: La Ligua 
Nombre Tienda: La Ligua 
Ip 1: 192.6.83.101 
Terminal_id : 20 
Store_id: 10283 
bm_ip: 192.6.83.244 
bm_url: http://192.6.83.244:8080/rs-bm-console-rs-bm-kiosco-server-abcdin/ServiceKioscoBean?wsdl
```
----

###Procedimiento

Con la información que se nos ha entregado, como primer paso verificaremos que exista comunicación desde los servidores de aplicación hacia la URL de BM con el siguiente comando:

`curl "bm_url"`

En el caso de no tener comunicación, se quedará pegado tratando de buscar comunicación y finalmente mostrará un error de conectividad.
**_Nota: No realizar la habilitación hasta que exista comunicación. Soporte Sistemas está al tanto de esto._**

Al tener comunicación se mostrará una serie de datos correspondientes al BM de la tienda.
![image.png](/.attachments/image-7a770251-db56-4972-a607-b014c4348d4e.png)

Nosotros tomaremos en cuenta solo el último extracto del mensaje, la siguiente línea:
![image.png](/.attachments/image-091140f9-9e75-417b-b56c-5173963a2216.png)

Esta url será la que utilizaremos para agregar al archivo hosts de **los 2 servidores de aplicación**. En el cual agregaremos los datos en el siguiente formato:

`bm_ip newpos_url newpos_nombretienda`

Ejemplo:
![image.png](/.attachments/image-d987fcdd-5ae1-48f8-a4b3-abbb30970997.png)

Luego debemos ingresar a la base de datos de Kiosko, con privilegios de admin.

[RDS_admin.rar](/.attachments/RDS_admin-92ef0186-b3c3-4de4-8f69-25a3dc40ac06.rar)

Crearemos la siguiente Query:

```
INSERT INTO kiosks (terminal_id,store_id,bm_url,created_at,updated_at,open,new_promo)
VALUES(20,10283,'http://192.6.83.244:8080/rs-bm-console-rs-bm-kiosco-server-abcdin/ServiceKioscoBean?wsdl',current_timestamp,current_timestamp,'true','true');

```
En donde, varía el Terminal ID,Totem ID y la BM_URL, (los primeros 3 parámetros) lo demás va por defecto. Podemos chequear también si necesitamos, en la tabla _kiosks_ para visualizar el formato.
*la tabla open sindica que la url está habilitada desde la base de datos*
*la tabla new_promo indica que la tienda se conecta al nuevo motor de promociones. Esta opción debería estar siempre habilitada si el Kiosko se encuentra operativo*

Luego de haber realizado el insert, podremos ver las tablas con la habilitación realizada.
![image.png](/.attachments/image-fcdbd5a4-f0c0-4593-9fa7-fa49d81e6843.png)

Con estos pasos realizados podemos dar el OK y documentar el ticket.

Si es que en algún momento realizan una tarea para cambiar una IP como la siguiente:
![image.png](/.attachments/image-5a0f182d-e73b-440f-8b14-388df07b74cd.png)

Los pasos son parecidos.
Se debe modificar la IP mencionada de la tienda que se indica en la base de datos y adicionalmente cambiar la IP en la tabla hosts de los dos servidores de aplicación.
*Recomiendo validar comunicación hacia la URL completa con esta nueva IP*
