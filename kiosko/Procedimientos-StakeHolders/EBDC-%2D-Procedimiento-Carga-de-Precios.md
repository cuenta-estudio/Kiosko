
**EBDC-Kiosko-ProcedimientoCargadePrecios**
|**PROCESO**|_Carga de Precios_|
|--|--|
|**AUTOR**| @<17962A48-91CA-6013-93A7-25B88797E017> |
| **BUG** | #169 |

[[_TOC_]]

----

### **Objetivo** :dart:
El objetivo de este procedimiento es poder realizar la carga de precios manual en Kiosko. Este procedimiento sirve tanto para el
momento de cargar precios para una nueva tienda o a modo de mitigación en caso de incidencias.
Carga de Precios via SFTP: Este procedimiento gatilla una carga de precios desde el **Worker** y dado el formato que requiere,
esta carga considera precios y fecha de vigencias para productos, por tienda


**check list ayuda para actividades** :white_check_mark:

- [X] validar conexión path SFTP
- [X] revisar formato archivo
- [X] revisar formato nombre archivo Unidad de Precios
- [X] considera hora carga
- [X] cambiar nombre archivo para worker


**diagrama secuencia de actividades** :notebook:
::: mermaid
sequenceDiagram
participant ops as OPERADOR
participant sftp as SFTP
participant worker as IBM Worker
participant eCom	as eCommerce
  ops->>ops: valida archivo carga
	ops->>sftp: suber archivo precios
    loop busca archivos pendientes    
	  worker->>sftp: lee archivos pendientes  
    sftp-->>worker: recupera archivos  
    Note over worker,eCom: se ejecuta al minuto 00 de cada hora
	  worker->>eCom: actualiza precios!
  end
:::


----
## Carga de Precios

**Información**
> Para realizar este procedimiento se requiere crear conexión al servidor SFTP de Kiosko. Esto puede realizarse con el software Filezilla, WinSCP o cualquier otra herramienta que refiera a transferencia de archivos.

>Credenciales para acceso vía SSH o SFTP:
```
HOST=200.54.96.56
PORT=22
USER=Kiosko
PASSWD=UJmnb2q.,
```

>ruta de carga de archivos: `/home/Kiosko/procesados`

![34a84b935ba8ff9fbf30ce54ec122618.jpg](/.attachments/34a84b935ba8ff9fbf30ce54ec122618-0e82284b-ff72-40da-9bad-beb892c49f19.jpg)

### Puntos a considerar Previo a Carga:

>El formato del nombre del archivo de carga es el siguiente:

![fff19f1974414719a36057dc06abc2b6.jpg](/.attachments/fff19f1974414719a36057dc06abc2b6-c3de4286-eb19-46fd-b3ff-ae2443057401.jpg)


>Este formato se debe mantener siempre, de lo contrario puede que el **Worker** no identifique la carga.

> Los datos dentro del archivo de carga siempre deben venir en este formato y es de exclusiva importancia que la primera línea contenga los datos seleccionados a continuación

![dd4facd4809a9882002eda79f3d1254a.png](/.attachments/dd4facd4809a9882002eda79f3d1254a-2ab8077c-2cb4-4b22-ba6d-09c23628e541.png)

>   En el caso que la carga considere una cantidad muy grande de registros, podría llegar a fallar y en este caso sería necesario dividir el archivo inicial en partes. **Es de vital importancia que cada archivo que se genere, tenga el formato mencionado en la imagen anterior.**

:warning: **Importante** :warning:
> - El Worker Realiza la carga de precios al minuto 00 de cada hora, por lo tanto es necesario considerar siempre el horario previo a la carga. 
> - Es posible cargar más de un archivo simultáneamente al SFTP. Sin embargo, no los cargará todos al mismo tiempo,siempre considerará el nombre del archivo en orden de Fecha y Hora.

----
## Procedimiento Carga de Precios

>Es importante que dentro de el archivo de carga, se encuentre la tienda que requiere los cambios o carga de precios. Por ejemplo si la carga de precios va para la tienda 280, siempre en el archivo de carga irá el número de la tienda con un 10 previo, como correlativo.

![2bbf25a037d339d053b7e9de9b628d7f.png](/.attachments/2bbf25a037d339d053b7e9de9b628d7f-3ee5e4fb-450d-4407-b5cf-2c1325e78f00.png)

> Antes de cargar el archivo al directorio SFTP, se recomienda tomar en cuenta los archivos que ya han sido cargados en el directorio.
>_Es muy probable que Unidad de Precios nos envíe el archivo con un nombresimilar a este_: `CI_KIOSKO_20200206_1211.*`

>En caso de ser así o si es que tiene cualquier otro nombre, debemos validar que la información que contiene este archivo sea el correcto, luego de esto solo debemos cambiar el nombre al formato necesario.

![31bd39ddb36a9846d23c021643f7018d.jpg](/.attachments/31bd39ddb36a9846d23c021643f7018d-705753a6-9ce4-4f83-8862-c60e8d2ada62.jpg)

> Y según estos archivos, SIEMPRE CONSIDERAR LA FECHA, los correlativos previos y posteriores pueden cambiar. Por ejemplo, considerando la imagen anterior, el nombre podría ser el siguiente:

![65441fd45e7b2b3bb5f78da3c23e268c.png](/.attachments/65441fd45e7b2b3bb5f78da3c23e268c-a4d08716-7bc3-4ee7-8816-8915eccf3cb9.png)

> Luego realizaremos la conexión al SFTP.

![435f5f09a197cc2eef4c4f4d3f4f1c4b.png](/.attachments/435f5f09a197cc2eef4c4f4d3f4f1c4b-86966cc4-2cec-4fa0-89e1-f3171b5ffcf3.png)

> Una vez conectados, iremos a la ruta /home/Kiosko/procesados

![d7aeeae188a7e96c2ee4d7da4d94bb74.png](/.attachments/d7aeeae188a7e96c2ee4d7da4d94bb74-9f33d504-52fc-48d0-b66e-f298e76c12fa.png)

> En esta ruta es donde cargaremos el archivo de carga de precios. Esto lo podemos hacer arrastrando el archivo a la ruta.
> En caso de agregar más de un archivo, simplemente fijarse que las horas de carga vayan en orden, considerando el siguiente ejemplo:

![7b03c2599dd4ce8fec92887e1c203e20.jpg](/.attachments/7b03c2599dd4ce8fec92887e1c203e20-6d2c9cb5-83b4-4aed-8592-215087f93c40.jpg)

> Al realizar esto, la carga de precios ha sido realizada. Solo debemos esperar que el **Worker** detecte los archivos y los vaya procesando.
