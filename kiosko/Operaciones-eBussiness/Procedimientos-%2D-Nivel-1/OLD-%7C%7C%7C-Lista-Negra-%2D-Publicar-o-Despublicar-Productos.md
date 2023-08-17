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
- [X] Validar conexión a Servidores de Aplicación

----
##**Procedimiento**

###Tarea No Masiva

Una vez conectados al servidor de aplicaciones, ingresaremos con el usuario ubuntu y ejecutaremos el comando "blacklist", el cual nos arrojará a
un menú.
_Nota: para cambiar al usuario ubuntu ejecutar el siguiente comando: sudo su - ubuntu_

![image.png](/.attachments/image-c896f92e-56e0-4758-8d70-34452b03e102.png)

En este menú solo debemos ingresar la opción que se requiera y se ingresarán los productos de 1 en 1.

###Tarea Masiva

Se deberá ejecutar un comando específico en el servidor App1 con el usuario ubuntu, ya sea para la publicación o despublicación, en el cual se agregarán todos los SKU's involucrados, separados por coma y {}.

####Despublicación
Comando:

```
curl --header "Content-Type: application/json" --request POST --data '[{"sku": 12345},{"sku": 23456}]' http://localhost:4000/products/forbiddenProducts
```
####Publicación
Comando:
```
curl --header "Content-Type: application/json" --request DELETE --data '[{"sku": 12345},{"sku": 23456}]' http://localhost:4000/products/forbiddenProducts
```
####COMBO

Para despublicar productos COMBO desde el Kiosko es el mismo procedimiento, sin embargo es necesario eliminar la palabra "COMBO" como tal.

Ejemplo:

Combos a despublicar:
COMBO9970
COMBO9969
COMBO9968
COMBO9967
COMBO9966

Query de ejecución:

`curl --header "Content-Type: application/json" --request POST --data '[{"sku": 9970},{"sku": 9969},{"sku": 9968},{"sku": 9967},{"sku": 9966}]'http://localhost:4000/products/forbiddenProducts`


###Validación Lista Negra

Para validar que los productos estén en la lista negra o no, haremos un select a la tabla _forbidden_products_

`select * from forbidden_products ;`

![image.png](/.attachments/image-720bfeb6-9cca-4fb8-a6be-8438a606c7e6.png)