

Historia de usuario:
#61508

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Corregir problemas con productos que no muestran sus precios.

#Problema:
Algunos productos que se muestran en Kiosko a los usuarios se ven sin su precio normal, lo que no permite comprarlos. Esto se provoca cuando el producto no tiene un precio normal establecido en la tabla de precios de kiosko. 

#Solución:
Magento incluye el precio normal del producto, por lo que se ha mapeado para ser utilizado por el kiosko. Cuando un producto no tenga un precio normal establecido en la tabla de precios entonces utilizará el precio normal que viene de magento.


#QA


Los productos que no cuentan con su precio normal ahora no se están publicando en el kiosko tenemos la siguiente imagen como ejemplo 

![productos sin precio normal.png](/.attachments/productos%20sin%20precio%20normal-7c6898ec-3f92-415d-b882-9a43578d11c6.png)