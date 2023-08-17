| PROCESO | Recolección de Logs |
|--|--|
|  AUTOR| @<17962A48-91CA-6013-93A7-25B88797E017>   |


[[_TOC_]]

----

## **Resumen** 
:radio: El procedimiento a continuación, consta de los pasos a cumplir para cuando se necesite extraer algún log del Kiosko Físico.
Para esto hay que tener en cuenta los siguientes puntos:

- Se utilizarán Credenciales de Administrador, por lo tanto es necesario tener extrema cautela en no realizar modificaciones ni eliminar archivos.
- Si es que los Kioskos van rotando físicamente o se habilitan/deshabilitan Kioskos, las IP's van quedando desactualizadas y no será posible conectar. Por lo tanto, es responsabilidad de cada uno de nosotros mantener actualizado este documento. 
- El contacto directo para validar la IP de un Kiosko es Raul Diaz, del área de Operaciones Sistemas. También podemos consultar con Luis Ortega.

----

Info Adicional:


| *User* | *Password* |
|--| -- |
| ingycom | ingydeltadm |


----
## **IP Kioskos**

![image.png](/.attachments/image-79c54bb3-9505-4449-b755-7dfac633fba1.png)

Si necesitan el documento: [Listado IP Kioskos.xlsx](/.attachments/Listado%20IP%20Kioskos-37b62862-9259-4b6e-96df-48c072cb7212.xlsx)


----
## **Procedimiento**

Nos conectaremos al Kiosko que se necesite retirar algún mensaje de log conectandonos a la VPN.
![image.png](/.attachments/image-89f3b767-59e7-4f84-a9ad-df82961ee5c9.png)

Utilizaremos el Comando "Windows+R" o directamente a la opción "Ejecutar" desde nuestro pc, haciendo click derecho al inicio de Windows.
![image.png](/.attachments/image-e3ed0eac-1c2b-4980-8aeb-4c7eaff3aac8.png)

Aquí ingresaremos la IP, precediendo el doble backslash y haremos click en "Aceptar".
![image.png](/.attachments/image-8c74f15e-23e0-4054-a835-79118a9b64df.png)

El sistema requerirá de las credenciales de Administrador.
![image.png](/.attachments/image-94ef7f9b-c2e2-4350-b452-aa69f5c6a99a.png)

Luego de ingresar las credenciales ingresaremos al Kiosko, como recurso compartido.

![image.png](/.attachments/image-ec540927-44fa-45fa-9ff4-f3b28e889926.png)

La ruta central para identificar los logs es la siguiente:

_\\\192.2.96.101\kiosko096\lib\KIOSKO\VTOL_
![image.png](/.attachments/image-f5d36e0a-5050-4308-9187-1d15bb564404.png)

Uno de los logs que utilizamos se encuentran en la siguiente ruta:

_\\\192.2.96.101\kiosko096\lib\KIOSKO\VTOL\vtol-bridge-flow-1.0.0\bin_

![image.png](/.attachments/image-fa2d5036-b13f-4cc1-8bb1-7522ab783472.png)

El otro log se encuentra en la siguiente ruta:

_\\\192.2.96.101\kiosko096\lib\KIOSKO\VTOL\vtol-pos-client-lib-cl-1.3.2\log_

![image.png](/.attachments/image-eeda8f88-fdf2-41e5-952d-a79e6a1a06e3.png)

*IMPORTANTE*
Solo copiar los archivos y pegarlos en sus respectivos computadores. No cortar ni modificar el archivo, Tampoco leer el archivo desde el directorio compartido. Ya que el Kiosko se puede encontrar en uso y si se corrompe un archivo, se pueden generar errores.
