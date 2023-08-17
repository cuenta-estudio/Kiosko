| PROCESO | Validación Regla de Precios |
|--|--|
|  AUTOR| @<17962A48-91CA-6013-93A7-25B88797E017>  |

[[_TOC_]]

----

## **Objetivo** 
:dart: Este procedimiento se ha creado para validar la regla de precio sobre los productos, en Kiosko.

----
**Info** 
Se ha creado la tabla _configuration_price_worker_apps_ en la base de datos de Kiosko. En esta figura el porcentaje máximo que se le puede aplicar al precio vigente.
Actualmente se está aplicando la misma regla del commerce.
![image.png](/.attachments/image-3c9b5c1a-93e8-4cc3-ac73-c52bb1def65b.png)

Mayor información, lógica y detalles sobre el proceso completo, se adjunta el siguiente manual realizado por Acid Labs.
[Descripcion reglas de precios.pdf](/.attachments/Descripcion%20reglas%20de%20precios-cc068bb2-09f2-40f3-a132-a65cf79db142.pdf)

----

##Validación Regla de Precio sobre SKU

Este es el mensaje tipo, de un error común de regla de precio:
![image.png](/.attachments/image-5537e6ff-9491-4402-a4eb-4f55f717af32.png)

----
En el caso que se reporte algún problema de regla de precio, necesitaremos los siguientes datos:

- SKU
- Tienda Afectada

Con estos datos en mano, necesitaremos ingresar al servidor Worker de Kiosko. 

Luego de estar en el servidor, debemos estar conectados con el usuario ubuntu.
Iremos a la siguiente ruta: /home/ubuntu/.pm2/logs

![image.png](/.attachments/image-8ed25ddc-340d-41f7-aa8a-f80ea1e02abe.png)

Ya en el directorio, podemos ejecutar el siguiente comando:

`grep -ri -E -A5 'SKU|isPromoPriceValidDiscount'`

_Nota: este comando sirve solo como guía, pueden utilizar cualquier otro comando en bash que les funcione para encontrar lo mismo._

----
Esta línea nos mostrará bastante contenido. Dentro de esto, lo siguiente:

- Nombre del archivo que contiene el registro.
- Línea con información del Producto: Número de Tienda - SKU - Precio Normal.
- Descuento aplicado al producto, iniciando con el mensaje "isPromoPriceValidDiscount".
----

A continuación un ejemplo con el SKU 866687.

![image.png](/.attachments/image-af448236-723a-44fc-95c0-166e3a2d1fee.png)
![image.png](/.attachments/image-1df41c13-2353-4d15-b861-bf4aec01d15b.png)

Tener en consideración:
Luego de la información del SKU que estamos buscando, vendrá inmediatamente el mensaje de regla de precio, indicando el descuento que se
intentó aplicar.

Cada vez que aplique la regla de precio, se verá publicado en kiosko el producto con el **precio Normal**.

También podemos buscar por el mensaje de error como tal:
Ejemplo:
`grep -ri -E -A5 '1110122|the discount is bigger than the allowed'`
![image.png](/.attachments/image-39e28a0d-d5be-410b-a2d2-47dfe471b8ce.png)

O podemos buscar en un archivo específico, si tenemos la fecha en la que necesitamos buscar.
Ejemplo:
![image.png](/.attachments/image-bd9e835e-04a5-4755-b852-ed8630700e61.png)

`zgrep -i -A5 "the discount is bigger than the allowed" abcdin-price-worker-out-3__2020-06-04_00-00-00.log.gz`

![image.png](/.attachments/image-30f4b41b-36ed-48b0-81b7-93f84cef5084.png)

----
Con esta guía es posible realizar una primera validación, sobre si la razón de que el producto tenga un precio mayor al que indican por parte del negocio, figura así debido a que aplicó la regla de precios.

En el caso que sea necesario actualizar precios en el Kiosko, se deberá ejecutar el procedimiento de Actualización de Precios: 
https://dev.azure.com/ADretail/kiosko/_wiki/wikis/kiosko.wiki/73/Actualizaci%C3%B3n-Carga-de-Precios
