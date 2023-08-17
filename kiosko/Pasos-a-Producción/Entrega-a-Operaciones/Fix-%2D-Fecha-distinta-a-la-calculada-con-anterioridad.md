Historia de usuario:
#42028

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Implementar fix a problema que ocurre con las fechas de los despachos informadas por productos. 

#Problema:
Cuando el kiosko consulta por el despacho de los productos al servicio de shipping, envía todos juntos y es el servicio el que responde las fechas de todos los productos consultados, en conjunto con la fecha unificada.

Hay casos en que el servicio de shipping informó fechas distintas para productos dentro de la misma orden, no respetando la fecha unificada, y esto provocó un error al momento de realizar la consulta.

Actualmente el kiosko almacena la fecha informada en el producto y no la que se informa en la fecha unificada, lo cual no debería ser.
 

#Solución:
Para solucionarlo se asignó a los productos la fecha unificada, ignorando la informada individualmente por los productos, ya que todas deberían ser iguales que la unificada.

#QA

En el log de kiosko se puede visualizar la respuesta que entrega el servicio de shipping de la siguiente manera, donde incluye la fecha unificada

![wiky logs de shippin day .png](/.attachments/wiky%20logs%20de%20shippin%20day%20-cd347281-2f34-470c-82a1-04409260e444.png)

Y también lo podemos ver en la tabla order_product en la columna delivery_date de la siguiente manera, donde refleja el mismo valor que la fecha unificada:

![wiky tabla shippin day .png](/.attachments/wiky%20tabla%20shippin%20day%20-f907c64b-9edc-41d5-a3eb-a4ae4a90bd27.png)



