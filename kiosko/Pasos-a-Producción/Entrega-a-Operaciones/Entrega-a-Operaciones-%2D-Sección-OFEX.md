Historia: #4822

| Descripción | Modificaciones Front - Vista de Productos en Categoría, Precios y Ofex |
|--|--|
[[_TOC_]]

----
#Compendio Técnico


_A continuación se informan los siguientes cambios realizados a nivel de Desarrollo._

----
##QA
###I - Etiqueta para productos ofex
1. Se agrega img en /public
2. Se llama img en components/Prices/index.js
3. Se da estilos en Product.scss

###II - Se mejora vista de producto, se modifican estilos de precios y se agrega imagen de tarjeta
1. Se da estilos en ProductView.scss, tanto a precios, como img

###III - Al ingresar a una categoría, mostrar ofex al inicio y sin stock al final
1. Se realiza lógica en components/Catalog/index.js

###IV - Destacar precios solo de precios ofex:
1. Se da estilos a precios e img en los siguientes archivos, Product.scss, ProductView.scss, ShoppingCart.scss, ProductList.scss y choosePrices.js 

----

#Documentación Operaciones
_A continuación se entregará información relevante de acuerdo a las modificaciones realizadas, correspondiente a la Operación como tal. Vale decir: Diagramas de flujo asociados en caso de aplicar, validaciones a realizar en la Operación, tips de revisión, etc._

##Cambios FrontEnd

Se validan los siguientes cambios:

###Categoría
Al ingresar a una categoría, mostrar productos con Ofex al inicio y mostrar productos sin stock al final. Esto se verá reflejado de la siguiente manera:

Inicio:
![image.png](/.attachments/image-f3596f8c-ba7b-4e5b-98c4-45923ccd8c1b.png)

Final:
![image.png](/.attachments/image-d57f2d97-6f76-42b6-9e14-ae06eb3d0fed.png)

###Precios Ofex
Se destacarán sólo los precios Ofex. Así también se configuran los siguientes tamaños fuente:

- Precio ABCVisa: Color rojo - Tamaño grande
- Precio Vigente: Color negro - Tamaño Mediano
- Precio Normal: Color gris claro - Tamaño pequeño

Esto se visualizará de la siguiente manera:
![image.png](/.attachments/image-f122b81a-0985-4866-b916-c9cc1ca6b4a3.png)

###Logo Ofex
Se visualizará un logo de la tarjeta en los productos que poseen Ofex. 

Esto se visualizará de la siguiente manera: 
![image.png](/.attachments/image-ada0996d-931e-4ae5-bf38-738967a7bcad.png)

----

##Revisión Adicional

Una vez implementado en producción, adicional a la revisión visual en el FrontEnd, es posible visualizar los logs asociados al Front en los servidores de aplicaciones en las siguientes rutas:

_/home/ubuntu/.pm2/logs/abcdin-frontend-error-*.log
/home/ubuntu/.pm2/logs/abcdin-frontend-out-*.log_

Así también, es posible realizar la revisión vía pm2 dentro de los servidores de aplicación.
Usuario: ubuntu

- Comando _pm2 list_
- Luego _pm2 log abcdin-frontend_ ó _pm2 log "id de aplicación"_ 
![image.png](/.attachments/image-3b92c558-cdc9-419a-b9c9-36a7e7a08fae.png)

----
##Manual Técnico Paso a Producción
El Paso a Producción se estará llevando a cabo mediante el siguiente documento Técnico, en los servidores de Aplicación:

[Manual Tecnico Paso a Producción Front End](https://dev.azure.com/ADretail/kiosko/_wiki/wikis/kiosko.wiki/241/Manual-T%C3%A9cnico-Paso-a-Producci%C3%B3n-Front-End__06-10-2020)