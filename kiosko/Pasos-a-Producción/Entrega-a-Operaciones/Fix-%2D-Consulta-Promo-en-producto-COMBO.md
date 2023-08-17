Historia de usuario:
#42119

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Implementar un fix para que los combos no consulten a motor promo, ya que genera descuadre en las ofertas de los combos.

#Problema:
Cuando el kiosko consulta por productos, primero va a buscar los productos a IBM, donde incluye algunos precios. Luego éste consulta al servicio de promociones para complementar los datos que tiene del producto con las promociones aplicables.

Este comportamiento no aplica para los combos, ya que las ofertas de estos se configuran directamente en ibm, al consultar en promo se generan conflictos al determinar cual descuento aplicar. Los combos ya tienen todo su detalle de precios configurado en ibm, no se debe consultar al servicio de promos. 

#Solución:
Se implementó un filtro al momento de buscar productos y consultar en el servicio de promociones, que quita los sku de combos de la consulta. 

#QA

#Luego de colocar el filtro para los combos podemos visualizar la inexistencia de promociones en combos sin OFEX de la siguiente manera en:



Boleta:

![Captura de pantalla 2021-08-16 153420.png](/.attachments/Captura%20de%20pantalla%202021-08-16%20153420-470938da-b4ad-419d-b5e4-aab8942cd034.png)

Y en el Tlog de la siguiente manera:

![Captura de pantalla 2021-08-16 153913.png](/.attachments/Captura%20de%20pantalla%202021-08-16%20153913-536f646e-ee39-4ce7-9b42-8b6a02500b4f.png)![Captura de pantalla 2021-08-16 154004.png](/.attachments/Captura%20de%20pantalla%202021-08-16%20154004-bfa1a17e-4456-4a8c-b2fe-edb821da9a24.png)![Captura de pantalla 2021-08-16 154040.png](/.attachments/Captura%20de%20pantalla%202021-08-16%20154040-86f05f92-adf4-4332-aa09-6bd18050bf8b.png)



   #Por otra parte también podemos ver los descuentos correctos con OFEX de la siguiente manera  



En la boleta
![con ofex bol.png](/.attachments/con%20ofex%20bol-a6b8495b-a24c-49d9-8e1e-63911c41c027.png)


Y en el Tlog de la siguiente manera 

![con ofex tlog 1 .png](/.attachments/con%20ofex%20tlog%201%20-1f34ef89-c53a-4d08-8765-a43a2d4ce5c0.png)![con ofex tlog 2.png](/.attachments/con%20ofex%20tlog%202-221bb0aa-5e03-40d6-9b12-35f8c3c908cf.png)![con ofex tlog 3.png](/.attachments/con%20ofex%20tlog%203-67a65ba7-29a8-45f9-aaf8-02de4ae8b315.png)




