| PROCESO | Regeneración de TLOG |
|--|--|
|  AUTOR| @<17962A48-91CA-6013-93A7-25B88797E017>  |


[[_TOC_]]

----

## **Objetivo** 
:dart: El objetivo de este procedimiento es poder realizar la mitigación de regeneración de TLOG, para los casos en que el XML no se ha generado y es necesario su reinyección.

----
## Info
El endpoint para poder regenerar el tlog mediante un numero de folio es:

`https://{host}/api/orders/{folio}/tlog/regenerate`

----

Ejemplo: 

https://app.abcdin.cl/api/orders/123456/tlog/regenerate

En donde "123456" sería el número de boleta a regenerar.

----

Esta ruta está protegida por usuario y contraseña, los cuales serán requeridos por el navegador.

User: abcadmin
Password: abcadmin

----
Se adjunta a continuación el procedimiento para la regeneración de Tlogs, entregado por Acid Labs, para más detalles.

[Regeneración TLOG.pdf](/.attachments/Regeneración%20TLOG-2cc13604-24a8-4f92-879a-9791627cdadf.pdf)
