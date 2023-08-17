Historia de usuario:
#51963

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Enviar boletas por correo a los clientes que así lo quieran, esta es una opción a imprimir la boleta.

#Problema:
Actualmente en el kiosko solamente se puede imprimir la boleta, por necesidad de negocio se necesita añadir la opción de envío de boleta al correo electrónico de la persona.

#Solución:
Se modificó el flujo al finalizar el pago, ahora se derivará a pantalla para imprimir o enviar boleta por correo. Para esto se debió implementar un módulo en la aplicación para el envío de los correos mediante SMTP, además de implementar sistema para re intento de envío.

Se han realizado las siguientes modificaciones:
- Ahora no se imprime la boleta automáticamente al finalizar el pago, ahora solamente se deriva a nueva pantalla.
- Se añade nueva pantalla para imprimir o enviar boleta al correo.
- Se implementa módulo de envío de correo en app, mediante SMTP de AWS.
- Se almacena registro de correos enviados en tabla emails_registers
- Se implementa cronjob para re intento de correos.
- Se añadió teclado para ingreso de correo.
- Ya quita la validación de impresora antes del pago (ya no aplica).
- Se implementa servicio para generar pdfs con la boleta.


A continuación detallo los servicios implementados:

###FRONTEND
En el frontend, se añadió la siguiente página, para gestionar la boleta, donde se indica el folio y la opción de ingresar su correo o imprimir la boleta directamente:
<IMG  src="https://dev.azure.com/ADretail/011d8dea-f234-46e0-85d0-332f7664da67/_apis/wit/attachments/2119a3aa-cfbb-4115-a637-3ec30df24421?fileName=image.png"  alt="Image"/>

Adicionalmente se añadió el teclado con los carácteres necesarios para ingresar un email:

<IMG  src="https://dev.azure.com/ADretail/011d8dea-f234-46e0-85d0-332f7664da67/_apis/wit/attachments/ae54764e-51a4-4f9d-91e3-fdff85b42fd8?fileName=image.png"  alt="Image"/>

Cuando se envía o imprime la boleta, termina el flujo de la venta y se limpia la data para pasar a la siguiente venta:

<IMG  src="https://dev.azure.com/ADretail/011d8dea-f234-46e0-85d0-332f7664da67/_apis/wit/attachments/48afbc63-7d43-40d8-a473-afce64f7ca96?fileName=image.png"  alt="Image"/>

###BACKEND

En el backend, se implementó un endpoint para el envío de los correos, se puede acceder a este mediante:

POST
{url_kiosko}/voucher/{order-id}/email

Donde debes reemplazar las variables url_kiosko y order_id por las correspondientes. Este endpoint recibe en el body la siguiente data:

```
{
   "vouchers": [
        {
            "Type": "boleta", //boleta, voucher, etc
            "Content": txt_in_base64        
        }
    ]
}
```

Esto tomará la data de la orden indicada y completará la información faltante para enviar el correo. El array de vouchers contiene los tickets que se enviarán por correo como adjuntos. Cada uno corresponde a un tipo de boleta, y se genera un pdf en el backend para cada uno, este se convierte a base64 para no generar archivos en el sistema y para ser enviados por correo utilizando el servicio de AWS (SES).

Los emails son guardados en la tabla emails_registers, la que registra los datos necesarios para enviar el correo, incluyendo toda su data, template, si fue enviado, cuantas veces se ha re intentado, etc.

(imagen de bd pruebas qa)
![image.png](/.attachments/image-a24cbf44-2c4a-4333-b3dc-1a262e6a5371.png)

Cuando un email no se puede enviar por X motivo, se registra esto en la tabla en el campo failure y se marca para re intentar en el cronjob.

###CRONJOB
Para re intentar el envío de correos, se añadió un cronjob al app para obtener los emails que han fallado y tienen re intentos disponibles, este job utiliza el mismo servicio utilizado anteriormente por lo que no hay variaciones al respecto. 
El cronjob se ejecuta cada 1 hora, y realiza 24 re intentos para completar 1 día de re intentos (24 re intentos * 1 hora).

###EMAIL
El Email enviado contiene el folio de la venta, la fecha y la persona que se ingresó en el despacho. Además, incluye las boletas correspondientes como archivo adjunto en formato pdf.



![boleta en correo1 .png](/.attachments/boleta%20en%20correo1%20-3393a615-2cb9-4034-aefe-8ce9529cc5a2.png)
#QA

Luego de los cambios realizados podemos visualizar como se envía la boleta en formato pdf correctamente a el email
![boleta en correo .png](/.attachments/boleta%20en%20correo%20-96ebf27a-23b4-4aff-b871-ad192df82f88.png)

También se valida la correcta impresión de la boleta pinchando en el botón Imprimir Boleta

![Boleta impresa.png](/.attachments/Boleta%20impresa-f13a1cee-8967-40d5-aeea-f4b7cb5f17f8.png)

El correcto funcionamiento del nuevo teclado 

![Teclado envio de boleta por correo .png](/.attachments/Teclado%20envio%20de%20boleta%20por%20correo%20-294b7a43-8d30-4071-90fe-3d07c0882ef8.png)

También podemos comprar la boleta enviada por correo y la boleta que guardamos en la base de datos para y validamos que es la misma 
![boleta recibida en correo .png](/.attachments/boleta%20recibida%20en%20correo%20-ca4e6b51-3b58-46c1-b96d-01d4b18f900c.png)![Boleta en base de datos.png](/.attachments/Boleta%20en%20base%20de%20datos-d2f44299-aa2b-4362-80b0-627b54266e58.png)
