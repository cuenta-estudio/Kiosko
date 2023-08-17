Historia de usuario:
#36937

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Corregir una serie de problemas de contabilidad que se producen por generar incorrectamente el TLOG. Dentro de este fix se incluyen varios problemas relacionados al TLOG y sus elementos internos.
#Problema:
Luego de un análisis en junto a negocio, se encontraron distintos problemas dentro de la formación del TLOG, lo que  provoca que haya inconsistencia a la hora de generar cuadraturas. Dentro de estos se encuentra:

a) Al comprar combos o varios productos, se añade una etiqueta Tender duplicada al TLOG, con datos que deben ir en otra sección.

b) Al comprar combos o varios productos, se enumeraba erróneamente los LineItems dentro del TLOG.

c) Se duplicaban los descuentos al re emitir boleta de los combos al momento en que se cancela por alguna razón un pago.

d) Se calculaba erróneamente el descuento de los productos en los combos.

#Solución:
Para cada uno de estos casos se detalla la solución implementada:

a) Se eliminó la instrucción que duplicaba la etiqueta Tender. Ahora solamente aparece donde corresponde, no se duplica.

b) Al terminar de construir los LineItems en el backend, se re enumeran para corregir inconsistencias, por lo que ahora ya quedarán bien enumerados en el TLOG.

c) Se corrigió un fragmento de código que debía almacenar los order_product_id de los productos del combo, con esto se eliminan los anteriores y se registra solo los de la compra efectiva.

d) Se aplicó la regla de precios señalada por negocio, la cual consiste en que el valor de oferta del combo, equivale a la suma de los valores de oferta registrados para cada producto que compone el combo. Y el descuento de cada producto corresponde al precio unitario menos el de oferta. 

#QA

Luego de hacer varias mejoras podemos visualizar lo siguiente 
# A) Se elimino la duplicidad de la etiqueta Tender y solo se visualiza al final 
![nodo tender 1.png](/.attachments/nodo%20tender%201-31700689-5ee3-4042-93ae-7e573d2c8341.png)


# B) Numeración correcta de LineItems dentro del TLOG

![SequenceNumber 1.png](/.attachments/SequenceNumber%201-2d0fea05-0760-41c0-a98c-66dd7c830078.png)![SequenceNumber 2.png](/.attachments/SequenceNumber%202-05a30ea3-ef3a-4e2d-b743-5cb38d3930a5.png)![SequenceNumber 3.png](/.attachments/SequenceNumber%203-d765a9fc-fcbc-4b2a-a5a3-d0d5bc641ff3.png)



# C) La duplicidad de los descuentos al re emitir boleta de los combos al momento en que se cancela por alguna razón un pago quedo de la siguiente manera:

En boleta:
![duplicidad de descuento boleta.png](/.attachments/duplicidad%20de%20descuento%20boleta-d0d931fb-bd22-4e58-8eac-dff7852db4f5.png)

En la tabla:
![duplicidad de ofertas en combo.png](/.attachments/duplicidad%20de%20ofertas%20en%20combo-b77ce277-5884-4b74-9a56-ecd6e3e1a44c.png)

# D)Y el calculo de descuento los productos en los combos se ven de la siguiente manera

![descuento correcto 1 .png](/.attachments/descuento%20correcto%201%20-d9d39827-1c52-45ce-a18b-c28de2da3399.png)![descuento correcto 2.png](/.attachments/descuento%20correcto%202-4dd4f139-318d-4d82-a371-2e1024f29cee.png)![descuento correcto 3.png](/.attachments/descuento%20correcto%203-4e511b9f-69f2-460f-95e6-edce001ba658.png)
































