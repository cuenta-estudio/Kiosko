

Procedimiento para sacar la boleta de una venta en Kiosko, exclusivamente cuando nos reportan desde Tienda que no se imprimió la boleta.

Endpoint S3 Kiosko:
https://s3.console.aws.amazon.com/s3/buckets/kioskopriv/?region=us-east-2&tab=objects

El filtro para buscar una boleta es:

El número de Tienda:
![image.png](/.attachments/image-efd52bfa-285c-4f12-98ff-bb562574b8ef.png)


Luego el número de terminal:
![image.png](/.attachments/image-0ae97759-894d-446b-a810-c4d91288806a.png)

Luego la fecha:
![image.png](/.attachments/image-936f24df-c30d-4281-96ee-b6dc3a7fd5bc.png)

Finalmente el número de transacción:
![image.png](/.attachments/image-258e5111-3c3b-4737-b076-c3d872f3d837.png)

Como podrán ver, en la parte superior izquierda podremos ver el path completo. Y dentro de este bucket se encontrará la boleta, junto con el Tlog y el voucher
![image.png](/.attachments/image-c30a6ac7-b571-417d-8794-8f86a85366b6.png)

Para descargar la boleta simplemtene pinchamos el recuadro de la boleta y le damos a la opción "Download".
![image.png](/.attachments/image-20dc2453-9511-434a-a210-0b344f034769.png)

Luego de esto, enviamos la boleta a quién la solicite.