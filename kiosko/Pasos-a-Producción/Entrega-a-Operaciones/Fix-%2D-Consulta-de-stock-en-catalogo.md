Historia de usuario:
#66424

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Reducir el tiempo de consulta del catálogo

#Problema:
Actualmente Kiosko cuando realiza consulta a catalogo, se realizan varias request hacia magento para consultar el stock individualmente de los productos. Esto, ya no es necesario, ya que magento está incluyendo el stock dentro de su respuesta de consulta de productos.

#Solución:
Se ha retirado el código que consultaba por el stock. Además, se ha mapeado el stock desde la respuesta de magento, por lo que se puede omitir el proceso anterior, agilizando las búsquedas.

#QA


Antes de la mejora realizada teníamos un tiempo de espera de catalogo de 12 segundos aproximadamente como lo podemos ver en la siguiente imagen 

![antes de la mejora de catalogo
 .png](/.attachments/antes%20de%20la%20mejora%20de%20catalogo%20-2a8f236c-6ab3-4250-afac-5498cea4aec9.png)


Luego de la mejora de carga de catalogo tenemos un tiempo de espera de 4 segundos aproximadamente como lo podemos ver en la siguiente imagen

 ![luego de la mejora de cargo de catalogo .png](/.attachments/luego%20de%20la%20mejora%20de%20cargo%20de%20catalogo%20-392c5ead-035c-4e7e-8e4c-c97a33a9b2b2.png) 