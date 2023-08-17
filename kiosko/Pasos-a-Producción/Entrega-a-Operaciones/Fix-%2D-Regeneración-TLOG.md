Historia de usuario:
#31375

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:

El objetivo del desarrollo realizado, es implementar un fix para que el TLOG se genere correctamente al momento de renegarlo.
 
#Problema:

Se realizó el análisis correspondiente del caso y se encontró que durante la regeneración del TLOG se tenían en cuenta todos los productos de la orden al momento de añadirlos a los campos line-item al XML. Dentro de esos productos, se encontraban los productos de tipo COMBO, que no tienen toda la información completa necesaria y no se estaban filtrando, por lo que provocaban un error al intentar utilizar atributos que no existen. 

#Solución:

La solución a este problema fue simplemente filtrar los productos, eliminando del cálculo a los productos de tipo COMBO, ya que estos no deben ingresar al TLOG.

Con este arreglo ya se logró generar el TLOG correctamente para los productos de tipo COMBO.


#QA

Luego de los cambios realizados podemos visualizar la regeneración de Tlog correctamente:

![wiky regeneracion tlog.png](/.attachments/wiky%20regeneracion%20tlog-8c8c79cc-f28a-49e0-b538-556dd34a9a88.png)![wiky regeneracion de tlog 1.png](/.attachments/wiky%20regeneracion%20de%20tlog%201-c2c689ee-c334-456c-8904-0f9e53a526e5.png)![wiky regeneracion de tlos 2.png](/.attachments/wiky%20regeneracion%20de%20tlos%202-14965a4e-00d5-4822-aa7f-a27974ad22c4.png)![wiky regeneracion de tlog 3.png](/.attachments/wiky%20regeneracion%20de%20tlog%203-889da27c-7523-4b99-bdfe-9e2083d3ce54.png)