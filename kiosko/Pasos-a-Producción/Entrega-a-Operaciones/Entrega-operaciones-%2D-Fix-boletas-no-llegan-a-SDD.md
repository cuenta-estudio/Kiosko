Historia: 
#28234

Autor: Camilo Alaniz


[[_TOC_]]

----
#Desarrollo
##Objetivo
El principal objetivo de este procedimiento es solucionar un problema con la cantidad de caracteres que ingresa el usuario en el campo "nombre recibe", que provoca que no se almacene correctamente en sdd.

##Problema:
El campo de nombre en el kiosko tiene un límite de caracteres distinto para cada servicio, el problema es con el servicio que almacena en sdd ya que el límite de caracteres que tiene es de 19, mientras que el servidor no maneja la cantidad de caracteres que se el envía al servicio. Esto provoca un error en el servicio de sdd indicando que algún campo no está bien formateado.

Se replico el error simplemente escribiendo más de 19 caracteres en el campo nombre del formulario del kiosko, lo que da un error en ese endpoint del backend, aunque no bloquea la aplicación, pero es el endpoint que confirma los envíos.

En la siguiente imagen se muestra el error en el apartado network del front:
![image.png](/.attachments/image-90a9efd4-c661-4a0d-96e4-31e85241ae76.png)

Mientras que en esta, el error que provoca en el backend:
![image.png](/.attachments/image-9c3e9b0f-1546-4898-b591-f1ac145b2771.png)

##Solución:
La solución por parte de negocio corresponde a cortar el nombre si superaba el límite de caracteres del servicio. Con esto el servicio no generaría conflictos. 

Por lo tanto se aplicó dicho cambio a nivel de código cortando (slice) el string del nombre en el momento en que se construye el body de dicha petición. Este cambio se aplicó en el momento antes de enviar la petición, por lo que no afectará al resto de los servicios.

En la historia de usuario se indicó que debía cortarse a 20 caracteres, pero esta cantidad provocaba el mismo error, por lo que se redujo a 19 caracteres.

##Para las pruebas
Se deben realizar pruebas de regresión y realizar el flujo de compras completo puesto que esto ocurría al finalizar la compra, cuando se confirma el envío de la orden.

----
#QA


Luego de la mejora en backend donde se envía la información a SDD las boletas o facturas llegan de la siguiente manera a SDD




La boleta:


 ![imagen 1.png](/.attachments/imagen%201-360679d6-81e3-439f-8879-5242cefd6f6f.png)



En SDD se recorta el nombre hasta los 19 caracteres la cual se puede visualizar se la siguiente manera ![imannn.png](/.attachments/imannn-18c4add3-bed1-4d99-9389-bb8fb6d48bb0.png)





