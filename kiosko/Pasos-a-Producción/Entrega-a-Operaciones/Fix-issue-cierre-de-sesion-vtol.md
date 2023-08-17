Historia: 
#4820

Autor: Camilo Alaniz


[[_TOC_]]

----
#Objetivo
El principal objetivo de este procedimiento es el de mitigar la aparición de errores en VTOL producto al manejo de las sesiones del mismo. A continuación se procede a detallar el problema y la solución.

##Problema:
En ciertos momentos de algunas compras se estaban generando errores con VTOL que según la evaluación realizada con el proveedor  corresponden al mal manejo del cierre de sesión, ya que esta se cerraba antes de que todas las operaciones de los servicios de backend terminaran. Lo que provocaba que la librería no pueda hacer las reversas de operaciones porque la sesión ya había sido cerrada (los logs que indican el problema se encuentran dentro de la historia).


Se intentó replicar estos errores en conjunto con el proveedor, pero no fue posible ya que ocurrían en momentos aleatorios, por lo que nos indicaron que el problema estaba en la forma en que manejamos el cierre de la sesión del kiosko y que debíamos esperar a que todos los procesos terminaran antes de cerrarla, ya que luego no es posible realizar acciones como una reversa por ejemplo.


Posterior a esto se realizó la evaluación del código por nuestra parte y se observó que efectivamente, la conexión se cierra cuando el kiosko recibe el evento "originalsale" que desencadenaba el cierre de la sesion y envía un evento para iniciar con los procesos en el backend, esto ocurre en este fragmento de código, donde se cierra la sesión y se llama a la acción "setPayed", que es la que indica que ya se ha realizado el pago.


![image.png](/.attachments/image-bc99ecfc-f375-4b07-a388-51f9a09e5743.png)


Se intentó replicar el error desconectando el pinpad, provocando errores con la lectura, con la clave, problemas de conexión, también se probó desconectando los backends, y no se logró replicar de ninguna manera. Durante el proceso del fix mencionado más arriba, se grabó un video en donde se muestra que algunas compras se realizaban correctamente, mientras que otras exactamente iguales provocaban el error. Esto fue enviado al proveedor para la evaluación también. Por lo que también se adjuntarán estos videos para dejar en evidencia el error y su comportamiento aleatorio.

https://drive.google.com/file/d/1gr5K3i4SIZgbSt5QA2KEY92jCJn6JiOf/view?usp=sharing


##Solución:
Se realizó un ajuste al código del frontend que interactúa con el pinpad, donde se añadió una acción para desencadenar el cierre de sesión una vez terminaran todos los servicios, con esto se mitiga la aparición de estos errores, dando tiempo a que todos los procesos de backend terminen satisfactoriamente antes de cerrar la sesión.

Para realizar este ajuste, se creó una acción dentro del frontend llamada "closePinpadSession", que es ejecutada cuando se han realizado todas las acciones correspondientes en el módulo "orchesta" que es el que interactua con los servicios de backend posterior al pago. 

Esta acción lo que hace es enviar un evento "close_pinpad_session" hacia el código que interactua con el pinpad, que es reconocido por este y le indica que debe cerrar la sesión. De esta manera la sesión se puede cerrar en el momento que nosotros lo necesitamos.


##Para las pruebas
Este desarrollo no afecta el flujo de la compra ni añade nuevas funcionalidades, por lo que para probarlo simplemente se deben realizar las pruebas de regresión correspondientes, ya que este cambio es transparente de cara al usuario y no afecta a nuestros servicios.


----
##Desarrollo/QA
###I - Se cambia el momento del cierre de sesion del pinpad.
**FrontEnd:**
1. La conexión del pinpad se cierra cuando orchesta termina sus procesos.
2. Se añade una action para desencadenar el cierre de sesión del pinpad.
3. La nueva action, es llamada dentro del modulo orchesta.


Luego de las mejoras realizadas podemos ver el buen funcionamiento de sus funciones como son el:

	Buen funcionamiento de los filtros   
![1.png](/.attachments/1-51bc1bd5-516c-4be8-b372-53feac7f6306.png)

![1.1.png](/.attachments/1.1-bf427cb7-95e6-4af2-8849-567486721430.png)









	Buen funcionamiento del motor de búsqueda: 
 ![2.png](/.attachments/2-d05ac701-b120-4c47-ac74-ba64d795746b.png)









	El carrito de compras:
 

![3.png](/.attachments/3-969d055c-3787-4d14-84fd-e4cebdc7a1c0.png)







	Las categorías:

 
 ![4.png](/.attachments/4-d7d66776-a130-41f1-b7b0-1c03c21c77e7.png)

![4.1.png](/.attachments/4.1-e435c681-c254-417d-9328-36bfc9ce6efb.png)










	Botón OFEX
 
![5.png](/.attachments/5-8851e337-3471-4536-bdb9-c85d710b3001.png)

![5.1.png](/.attachments/5.1-af8021fc-1469-4008-9fac-982f3c841fa9.png)

 

	Cambios de estados de compra 
 
![6.png](/.attachments/6-8222afb2-4a05-46bb-a461-6abbd2f42122.png)



	Correcta creación de Tlog y boleta electrónica 
 

 ![7.png](/.attachments/7-e0139d30-30d5-4ed0-9af6-11a3446f35b2.png)

![7.1.png](/.attachments/7.1-01e72ae5-9f31-4eb7-90eb-48f0ff3b7564.png)












	Compra OK 
 

![8.png](/.attachments/8-ba22ebab-038a-4e8a-892c-2a51558dc936.png)