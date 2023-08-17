Historia de usuario:
#43070

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Mostrar correctamente la descripción en los productos de Kiosko.

#Problema:
actualmente la categoría no se muestra en todos los productos, algunos no la incluyen, además se debe incluir al producto la descripcion "long_description" que entrega magento, ya que no se estaba usando.

#Solución:
Se ha mapeado el long_description a las categorías de producto, las cuales se ahora se mostrarán en el producto siguiendo la siguiente regla de prioridad. Si no está presente alguna, se mostrará la siguiente.

1 - long_description
2 - description
3 - short_description
4 - vacío

#QA

Luego de los cambios realizados podemos ver como si trae descripción en long_description y short_description toma como prioridad mostrar el long_description 

![con 2 descrp.png](/.attachments/con%202%20descrp-b5e8846d-4f42-4eb3-a2dd-16b8ddbaf4d5.png)

Se agregan 2 imágenes del mismo caso para que se logre leer mejor 

![leer 1 .png](/.attachments/leer%201%20-92bb12c5-ba5a-418f-be8c-7b5ff43ebde3.png)![leer 2 .png](/.attachments/leer%202%20-100ae225-d67d-4018-ab14-d912a438dd00.png)


También se puede visualizar en la siguiente imagen que si long_description esta vacío y trae short_description con información muestra la descripción de short_description

![short desc.png](/.attachments/short%20desc-c2012143-7619-49b4-9f04-95a7288d880b.png)

Se agregan 2 imágenes del mismo caso para que se logre leer mejor 


![leer 1.2.png](/.attachments/leer%201.2-1f3ff330-e267-4272-8629-cbbe0aa54c14.png)

![leer1.1.png](/.attachments/leer1.1-23a4a27b-18f1-415a-99c8-6d00d86d8bbe.png)



Por otro lado si trae las descripciones vacías no muestra ninguna descripción como se ve en la siguiente imagen 

![sin descrip.png](/.attachments/sin%20descrip-96ee1823-2cd3-4c91-9412-48197abe480d.png)
