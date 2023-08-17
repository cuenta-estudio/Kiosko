Historia: 
#4820

Autor: Ignacio Opazo


[[_TOC_]]

----
#Objetivo
El principal objetivo de este procedimiento es el de mitigar la diferencia entre el monto total y el iva que existe en el archivo boleta que genera Kiosco y el archivo TLOG, generando diferencias contables, dado que este ultimo calcula el total y el iva en base a los valores base de los items cuando estan dentro de un combo.

##Problema:
Cada vez que se realiza una compra de tipo Combo con Offex y pago con ABCVISA, el TLOG genera un total e IVA incorrecto, ya que no aplica los descuento por el concepto de oferta asociado al tipo de pago con tarjeta ABCVISA.

Al momento de realizar una prueba en desarrollo, el resultado es el siguiente:

![image.png](/.attachments/image-b560ebbf-f68b-48bc-b91b-837112bd3427.png)
![image.png](/.attachments/image-a5f5dcbd-e2a5-416e-8668-ba513bcfbc22.png)

##Solución:
Se realizo un ajuste en el código, en el generador de Tlog para tomar el monto correcto cuando existe una offex con abc visa. Esto genera que tanto el monto en boleta y tlog sean iguales, evitando el descuadre de la compra.
Para realizar este ajuste, se modifico el archivo formatTlogJson.js en el método "_buildTotal", que es llamado al momento de construir el tlog, generando la glosa dentro del Tlog para los campos <Total />





----
##Desarrollo/QA
###I Al realizar los cambios podemos ver que el Tlog y las boletas se generan correctamente

![1.1.png](/.attachments/1.1-0f09f15d-fac7-4c3b-b1a4-b7d1172c5c2d.png)![1.2.png](/.attachments/1.2-f10e63cb-5fa3-4d2e-b8c4-011793a476d3.png)
![1.png](/.attachments/1-d5ac64f2-9e6c-493b-9567-14107f93130a.png)

![2.png](/.attachments/2-ce79a769-02ac-4b06-804c-18168c439d4f.png)
 



