Qué hacer cuando reportan que no se cargaron los precios en Kiosko?

Validarlo con la siguiente Query en la base de datos Kiosko:

`select * from files_logs fl order by creation_date desc;`

Aquí veremos los archivos que han sido procesados.
Podemos validar el nombre del archivo y la fecha en que fue cargado el archivo al ftp.
![image.png](/.attachments/image-82c0303b-0ee9-4f5e-b429-ee78e712a918.png)

En esta misma query veremos si el archivo que se cargó fue procesado exitosamente, si se encuentra en proceso de carga, procsando o fallido.
![image.png](/.attachments/image-84a7ef9a-f6b7-4e38-8edb-f5fef0deeeaa.png)

Adicional a esto podemos ver la fecha que realmente fue procesado el archivo, diferente a la fecha en la cual llegó el archivo al ftp.
![image.png](/.attachments/image-ad490e3a-e7c1-434b-8188-4a49297bd33d.png)

En caso de que nos reporten que se realizó una carga de precio y que no ha sido procesado, y validamos que en la query no aparece el archivo de la fecha especificada, será necesario ingresar al Worker.

Host: ec2-18-224-200-94.us-east-2.compute.amazonaws.com
Puerto: 22
Usuario: creado en base a sus llaves privadas

Luego de ingresar al servidor, deben cambiar al usuario ubuntu.
![image.png](/.attachments/image-ce171481-4c04-48a5-a1dd-c384314dc0c5.png)

Listaremos los servicios con el siguiente comando y nos enfocaremos en el servicio abcdin-price-worker
`pm2 list`
![image.png](/.attachments/image-0ab9ea3b-dfdb-4cd3-8c29-d57ef5333cff.png)

Primeramente para ver los errores que tuvo el servicio ejecutaremos el siguiente comando:

`pm2 log abcdin-price-worker`
ó
`pm2 log "ID"`

se verán mensajes como los siguientes:
![image.png](/.attachments/image-2673a181-5704-425e-b348-1c7a5cff7542.png)

Lo importante es guardar esta imagen para poder informar el error.

Luego de esto reiniciaremos el servicio con el siguiente comando:
`pm2 restart abcdin-price-worker`
ó
`pm2 restart "ID"`

luego de realizar este comando, podemos validar nuevamente con la query si se está procesando el archivo. Es normal que se demore unos minutos. 
Podrás ver cuando el archivo es detectado por el Worker, lo comienza a bajar y luego lo procesa.

Con esto validado ya podemos dar aviso que se ha realizado la carga de precio.