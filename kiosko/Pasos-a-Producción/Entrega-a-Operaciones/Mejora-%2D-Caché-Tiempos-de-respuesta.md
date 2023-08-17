Historia de usuario:
#66439

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Mejorar el proceso de caché de categorías y catalogo.

#Problema:
Las categorías en Kiosko no se encuentran cacheadas, lo que provoca que cada vez que el kiosko consulte por las categorías, estas tengan un tiempo de carga de 3 segundos aprox.

El catalogo por su parte, si estaba cacheando los productos, pero los dejaba por un periodo demasiado prolongado, lo que evitaba que estos estuvieran actualizados por lo que se mostraban productos que no deberían de mostrarse.

#Solución:
Para las categorías, éstas se añadieron al caché y tienen una duración de 1 hora hasta que se actualizan. Esto mejora ampliamente la velocidad de la respuesta del servidor, por lo que de cara al usuario ya no se ve que estén cargando, permitiendo que kiosko sea más fluido.

Mientras que para catálogo, se redujo el tiempo de caché de 1 hora a 10 minutos, para mantener los productos actualizados.

A continuación se deja un diagrama a modo de documentación de cómo funciona el caché de los productos.


![Untitled Diagram.drawio.png](/.attachments/Untitled%20Diagram.drawio-31a06000-dc14-4623-bd7f-2cf2fb797bfa.png)

En la imagen anterior vemos el flujo que realiza la app, donde un usuario que está navegando en el kiosko realiza alguna búsqueda. Kiosko se comunicará con el backend de Kiosko y le enviará la consulta más el id del kiosko, backend realizará la consulta con estos parámetros.
Si una consulta, ya ha sido ingresada anteriormente para el mismo Kiosko, entonces backend buscará los productos directamente en caché, en caso de no haber productos en caché, o ya haya expirado su duración, entonces el backend buscará los productos a Magento.

#QA


Luego de los cambios realizados con los tiempos de respuesta de cache, cambio notablemente los tiempos de espera ya que si otra persona en cualquier kiosko abre una categoría esta queda cargada en el servidor lo cual hace que los tiempos de espera sean menores para todos los kioskos 