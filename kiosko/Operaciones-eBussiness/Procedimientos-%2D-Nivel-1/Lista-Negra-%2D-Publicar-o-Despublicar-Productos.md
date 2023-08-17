| PROCESO | Publicar o Despublicar Productos |
|--|--|
|  AUTOR| @<17962A48-91CA-6013-93A7-25B88797E017>  |


[[_TOC_]]

----

## **Objetivo** 
:dart: El objetivo de este procedimiento es poder realizar la tarea de despublicación o publicación de productos en Kiosko._

----
## **Info** 

:information_source: Lo que ocurre internamente en este proceso cuando se requiere despublicar un producto, es que se llevan los SKU's a una lista negra, los cuales quedan alojados en la tabla _forbidden_products_ en la BD de Kiosko.

Esto quiere decir,  cuando se requiera volver a publicar un producto, se estará quitando el SKU de la lista negra.

----
 **Check list accesos** 
:white_check_mark: Para realizar esta tarea, es necesario contar con los siguientes accesos:

- [X] Validar conexión RDS
- [X] Tener instalado el Software gratis Postman
- [X] Ingresar la ip individual de cada uno en los grupos de seguridad del Nginx en Amazon
----
##**Agregar IP en Amazon**
Por temas de seguridad, fue necesario bloquearla llegada al Nginx desde internet. Por esta razón es necesario agregar nuestras ip a los grupos de seguridad del Balanceador para poder ejecutar el Postman exitosamente.

En amazon buscaremos el servicio "EC2".
![image.png](/.attachments/image-d4b48fb4-342b-4aa3-8132-fa2c59c85bc7.png)

Vamos a "Instancias" y buscamos por "nginx".
![image.png](/.attachments/image-0c8a1de0-fcfc-460d-8d72-f8715f754194.png)

Seleccionamos la casilla correspondiente a la instancia "ABCDin - Kiosko - Nginx - PROD"
![image.png](/.attachments/image-da452643-9d05-44fc-854e-1292ac30648a.png)

Iremos a la pestaña "Seguridad" de la instancia seleccionada y haremos click en el link del grupo de seguridad.
![image.png](/.attachments/image-9b0c0db3-1760-4220-9b4d-252a8db0d1c0.png)

Editamos las reglas de entrada.
![image.png](/.attachments/image-8b236413-21ec-41c6-a8ca-00376f78ad3a.png)

Agregamos una nueva regla.
![image.png](/.attachments/image-e38751ac-5e11-4aad-af8c-0c023c99f732.png)

Agregamos los siguientes parámetros:
![image.png](/.attachments/image-819d2bc2-9115-4b45-99a0-9a5a7c363339.png)

Y en la opción "Custom" agregaremos nuestra propia IP.
![image.png](/.attachments/image-cbf1060b-69f9-41d5-a633-7bd65c163433.png)

Esto ingresará la ip que tenemos en el momento.
![image.png](/.attachments/image-fd284235-777a-4bb5-aaf1-c2641647bf75.png)

Finalmente salvamos los cambios.
![image.png](/.attachments/image-44f7f3f3-373a-420f-b697-79e30de8d839.png)

*Cada vez que cambiemos la IP será necesario realizar este procedimiento y actualizar la IP*

##**Configuración Postman**

Archivo de configuración Postman con tareas Kiosko: [Kiosko.postman_collection.json](/.attachments/Kiosko.postman_collection-ae466bd2-54d3-423a-9123-8d1c56984ed1.json)
Settings Postman:
![image.png](/.attachments/image-9a6bd4e0-53be-4731-aca9-dcb6f2df0bc2.png)

----

##**Procedimiento**

Tanto para publicar como para despublicar, usaremos estos 2 postmans:

![image.png](/.attachments/image-150fb034-ca6d-428e-99a5-de72194e922d.png)

Solo tendremos que agregar los SKU's en el formato que viene por default en el template y luego hacer click en cl botón "send".

![image.png](/.attachments/image-32ffb30f-f345-49d4-b4b7-1681920d7ef6.png)

Veremos que esto se realizó correctamente porque la respuesta debería ser la siguiente:
![image.png](/.attachments/image-eef5ffd2-e7e5-4e11-ade3-a49d4df43937.png)

también podemos validar en la base de datos con la siguiente query:

`select * from forbidden_products fp order by created_at desc;`

![image.png](/.attachments/image-0b52f240-0881-48d1-89a3-710541cb0fa9.png)

Y para volver a publicar usaremos también el indicado:

![image.png](/.attachments/image-dd770dfc-7bb2-4f6c-9577-7695dfcf9802.png)

realizando la validación de la misma manera.

####COMBO

Para despublicar productos COMBO desde el Kiosko es el mismo procedimiento, sin embargo es necesario eliminar la palabra "COMBO" como tal.

