Historia de usuario:
#50091

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Mostrar en al cliente solamente productos que tengan despacho a domicilio.

#Problema:
Actualmente Kiosko permite la venta de productos que no poseen despacho a domicilio provocando problemas. Esto no debería ocurrir, ya que solamente deberían mostrarse los productos que si tengan despacho a domicilio.

#Solución:
Para la solución se realizó un filtro de los productos al momento de consultar a magento, por lo que solamente pasarán los productos que tengan despacho a domicilio.

#QA

Luego de los cambios realizados podemos ver como al quitar el despacho a domicilio en magento el producto desaparece de kiosko:

En la siguente imagen se muesta como se ve el producto cuando tiene despacho a domicilio activado 

![3.1.png](/.attachments/3.1-e4d59765-486a-4688-8dd7-44295d92104b.png)


Luego le quitamos el despacho a domicilio en magento:


![3.3.png](/.attachments/3.3-e1391fce-834d-41a5-aa5b-338a86b0d3e9.png)

Y de esta forma el producto desaparece de kiosko:

![3.4.png](/.attachments/3.4-4d969c85-ccfd-4e5c-88d9-5d511df83756.png)


   También se validaron 

#El parámetro Quantity que luego de dejarlo en 0 el producto aparece como producto agotado:

Asi se ve el producto con Quantity mayor a 0 

![2.2.png](/.attachments/2.2-2b3aa979-1b26-486c-b8a8-831e600ed4c2.png)


Y luego de dejar Quantity en 0 se ve de la siguiente manera

![2.4.png](/.attachments/2.4-87a1dcf4-5e94-4b77-9bd0-00d5706d99e2.png)

#El Parámetro Stock status se valida que si esta en Out of stock se muestra como producto agotado:

Se cambia el parámetro Stock status:

![STATUS4.png](/.attachments/STATUS4-89f2173b-0eee-466a-8e40-f002774420ac.png)

Y luego el producto se muestra de la siguiente manera 

![2STATUS.png](/.attachments/2STATUS-9cdc7c2b-fb68-4b5e-b20e-15c7fa12d644.png)