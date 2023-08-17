Relacionado al desarrollo de:
Fix Offex Combo Calculo Iva y Total TLOG


Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:

El objetivo del desarrollo realizado, fue implementar un fix para almacenar correctamente los datos de la compra de Combos en la tabla price_promotions, ya que actualmente estos no son almacenados produciendo una inconsistencia.
 
#Problema:

Se realizó el análisis correspondiente del caso y se encontró que el problema estaba en los productos de tipo combo con ofex, ya que el backend no tenía implementada una forma para añadir las promociones correspondientes al combo de ofex, al no tener promociones, no se registraban en la tabla "price_promotions" y debido a eso no se generaba correctamente el TLOG, esto provocaba que al re imprimir la boleta electrónica hubiera un descuadre entre el total y el monto pagado.

#Solución:

Para solucionar estos problemas, se corrigió en el backend la parte del código en que se añaden las promociones, añadiendo la promoción correspondiente a cada combo. Se debió calcular la diferencia entre el valor del combo con el del valor total sin descuento, para obtener el descuento del combo, y con esto repartirlo entre sus productos al momento de guardar en la tabla.

El calculo del descuento por cada producto del combo, era importante ya que es el que se utiliza en el TLOG para re emitir la boleta.

Además, se implementó el caso de los combos con ofex en el middleware formatTlog, para añadir correctamente el valor del descuento cuando se compran combos sin ofex, con tarjeta abcvisa.




#QA 

Luego de los cambios realizados podemos visualizar la correcta creación de :

Boleta:
 ![wiki boleta.png](/.attachments/wiki%20boleta-93fb3e01-230e-4e12-8aff-4574c97267d5.png)

Tlog:
![wiky tlog 1.png](/.attachments/wiky%20tlog%201-1781acee-48a6-4bce-84ee-16c5f305357d.png)
![wiky tlog 2.png](/.attachments/wiky%20tlog%202-c8e02371-ba9f-4194-a6e5-51f44ad8b6be.png)
![wiky tlog 3.png](/.attachments/wiky%20tlog%203-6734b916-27b4-4386-914c-e7a6380c5501.png)

Boleta Electronica:
![wiky boleta electronica.png](/.attachments/wiky%20boleta%20electronica-47c34af9-69e0-4b4e-9197-959dd87ec831.png)
