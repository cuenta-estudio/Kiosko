Historia de usuario:
#66421

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Corregir problemas de carga de kiosko cuando se vuelve a la pagina home.

#Problema:
Cuando kiosko realiza un redireccionamiento a la página de Home, este realiza una carga de la app nuevamente lo que provoca un problema en la interfaz en que se ve la app cargando y demora un par de segundos en ser funcional.

Esto es provocado por un problema del código al redireccionar las páginas, ya que se utilizaba el redireccionamiento del navegador y no el propio de React. 

#Solución:
Se corrigió el código del redireccionamiento, ahora se utiliza el correspondiente para aplicaciones React, por lo que ya no hay tiempos de carga cuando se llega al home nuevamente.

#QA


Antes de realizar las mejoras el tiempo de espera de 12 segundos para volver a el Home como se muestra en la siguiente imagen 

 ![sin mejora vuelta a home.png](/.attachments/sin%20mejora%20vuelta%20a%20home-2334184e-ebd1-446b-9a09-603c21249df7.png)


Luego de la mejora el tiempo de espera bajo a 5 segundo para volver a el home como lo podemos ver en la siguiente imagen 

![MicrosoftTeams-image (4).png](/.attachments/MicrosoftTeams-image%20(4)-170bfc32-0be8-4bee-9b93-d4aa5549a2ce.png)