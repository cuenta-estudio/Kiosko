
Historia: 
#30032


Autor: Camilo Alaniz


[[_TOC_]]

----
#Desarrollo
##Objetivo
El principal objetivo de este procedimiento es implementar el nuevo agente de NewRelic en los distintos servicios que involucran al Kiosko. Dentro de los que se incluye Frontend, Backend, Promo, Worker Cache y Worker Price.

##Procedimiento:

Se comenzó siguieron las instrucciones que se encuentran en la documentación de NewRelic básicamente, se realizó la instalación mediante el archivo de configuración newrelic.js en cada uno de los archivos.

Se añadió al archivo de configuración un token en el nombre de aplicación, que se reemplaza durante el despliegue por el nombre correcto según el ambiente en que se encuentra. En los ambientes de producción, este cambio se debe realizar de forma manual.

Dentro de cada servicio, se debió instalar adicionalmente la librería de nodejs especificada en la documentación para los ambientes de backend, mientras que para el frontend se debió de realizar la configuración mediante el Snippet de código generado desde la interfaz de New Relic.

##Desarrollo/QA

Luego de las mejoras realizadas podemos ver el buen funcionamiento de sus funciones como son el:

	Buen funcionamiento de los filtros   
![1.png](/.attachments/1-51bc1bd5-516c-4be8-b372-53feac7f6306.png)

![1.1.png](/.attachments/1.1-bf427cb7-95e6-4af2-8849-567486721430.png)


	Buen funcionamiento del motor de búsqueda: 
![2021-04-20 18_25_03-ABCDin.png](/.attachments/2021-04-20%2018_25_03-ABCDin-a1419bfe-5a39-4642-a0dc-f7a42a5de881.png)


	El carrito de compras:

![2021-04-20 18_26_11-ABCDin.png](/.attachments/2021-04-20%2018_26_11-ABCDin-8f6813c4-9327-44b1-b8ba-677c6ecb4599.png)

	Las categorías:

 
 ![4.png](/.attachments/4-d7d66776-a130-41f1-b7b0-1c03c21c77e7.png)

![4.1.png](/.attachments/4.1-e435c681-c254-417d-9328-36bfc9ce6efb.png)


	Botón OFEX
 
![5.png](/.attachments/5-8851e337-3471-4536-bdb9-c85d710b3001.png)

![5.1.png](/.attachments/5.1-af8021fc-1469-4008-9fac-982f3c841fa9.png)


	Cambios de estados de compra 


![2021-04-20 18_45_32-pgAdmin 4.png](/.attachments/2021-04-20%2018_45_32-pgAdmin%204-a15b3649-16b0-4007-9a0b-9a54de3e281a.png)

![2021-04-20 18_50_27-pgAdmin 4.png](/.attachments/2021-04-20%2018_50_27-pgAdmin%204-9b7382a0-b482-4d99-86f8-fe3054aa2967.png)

	Correcta creación de Tlog y boleta electrónica 
![222222.png](/.attachments/222222-f198847e-e186-4948-a6ef-fb9a5f06fc7e.png)


![11111111.png](/.attachments/11111111-ab0af42b-d51a-4721-aa48-e91a38fcac90.png)



	Compra OK 
![2021-04-20 18_35_47-ABCDin.png](/.attachments/2021-04-20%2018_35_47-ABCDin-e686c497-1344-4865-a73a-81c211e9c4a3.png)

	Por otra parte el nuevo agente de NewReli nos muestra lo siguiente 

![MicrosoftTeams-image (1).png](/.attachments/MicrosoftTeams-image%20(1)-890abd2f-88b0-4bd2-b74f-b6b0d405ea8e.png)
![MicrosoftTeams-image (2).png](/.attachments/MicrosoftTeams-image%20(2)-bf86fb3f-f616-42f4-bcc9-07d515a7ecc3.png)
![MicrosoftTeams-image (3).png](/.attachments/MicrosoftTeams-image%20(3)-89dc18f7-6abf-472f-bc7a-a5592c13f614.png)
![MicrosoftTeams-image (4).png](/.attachments/MicrosoftTeams-image%20(4)-ab06465a-b60b-4c25-8910-d0635f798aac.png)
