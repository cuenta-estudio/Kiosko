| PROCESO | Carga de Campañas |
|--|--|
|  AUTOR| @<17962A48-91CA-6013-93A7-25B88797E017>  |


[[_TOC_]]

----

## **Objetivo** 
:dart: Cuando se programan Campañas para el eCommerce, el área de Marketing generará Banners de las mismas campañas con un template adecuado al Kiosko y se hará el requerimiento para cargarlo a la plataforma.

Actualmente se están cargando campañas en 2 formatos:
- Búsqueda por Categoría: Una vez que el cliente haga click en la imagen, esta redireccionará a la categoría que se haya indicado, la cual corresponde a una categoría existente en el Commerce.
- Búsqueda por Keyword/Término: Una vez que el cliente haga click en la imagen, esta redireccionará al keyword que haya sido configurado previamente. Este Keyword podría redireccionar tanto para una categoría, como también para un conjunto de productos y/o categorías, según haya sido configurado. Este corresponde a un keyword existente en el Commerce.

_Nota: Kiosko siempre consume los mismos servicios que el eCommerce._

----
 **Check list accesos** :white_check_mark:

- [X] Validar conexión RDS
- [X] Validar conexión a Base de datos eCommerce - Live
- [X] Validar acceso a S3 - AWS
- [X] Validar conexión a Simulador Kiosko
- [X] Validar Software "Postman" instalado
Archivo de configuración Postman para carga de campañas: [Kiosko.postman_collection.json](/.attachments/Kiosko.postman_collection-0b9f4c3d-c6a8-4a59-afa3-9bc264241b40.json)
Settings Postman:
![image.png](/.attachments/image-9a6bd4e0-53be-4731-aca9-dcb6f2df0bc2.png)
----
## **Información Necesaria Stakeholders** 

:information_source: Para proceder con la actividad necesitaremos los siguientes datos de parte de los stakeholders:

- Imágenes Adjuntas correspondientes a cada campaña.
- Definición del producto digital al que se cargará la campaña (Kiosko - App).
- Indicar la fecha de vigencia de cada campaña (Fecha inicio - Fecha fin).
- Indicar el formato de búsqueda para cada campaña.
Dependiendo del formato de búsqueda, se solicitará lo siguiente:
- Búsqueda por Categoría:
  - Nombre de la categoría en el eCommerce.
  - URL de la Categoría en el eCommerce.
- Búsqueda por Keyword:
  - Nombre de Display para el motor de búsqueda.
  - Keyword.

##**Pasos a Realizar**

Los pasos para la carga de campaña son los siguientes:
- Publicación de Campaña en S3 - AWS.
- Carga de Campaña vía Postman.
- Validación de Campaña - Emulación Kiosko.

##**Procedimiento**

###Publicación de Campaña en S3
Descargaremos los banners que adjunten en el ticket.
![image.png](/.attachments/image-ad473784-23fb-4720-8bff-baed5ec93355.png)

Ingresaremos al S3 de AWS al bucket _kioskopublic_.
![image.png](/.attachments/image-c4e636ee-17d8-4495-ae08-a4b9721cb20d.png)

Dento de _kioskopublic_ crearemos un bucket por cada Campaña que se deba cargar.
La nomenclatura que usaremos para la creación del bucket será la siguiente:
**Número del ticket - letra "K" o "A" (kiosko o app) - Nombre de Campaña/Banner**

![image.png](/.attachments/image-35c044ee-bf2b-464c-b0d4-167136b9177f.png)

Luego de creado el bucket, cargaremos la imagen a este. Se puede hacer arrastrando el archivo directamente o con la opción "Cargar" que tiene
el bucket.
Luego de cargado, haremos nuevamente click en _"Cargar"_.
![image.png](/.attachments/image-3343ff55-8193-4122-b4e0-e4485d627bf2.png)

Una vez cargado se verá de esta manera.
![image.png](/.attachments/image-f9feb69e-7fa2-44ee-a0bc-317bfa45f335.png)

Haremos click en el checkbox _Acciones_ Hacer público.
![image.png](/.attachments/image-121628d1-f84d-4178-a3ee-7b2f59a7dfcf.png)

Se desplegará un prompt, al cual le daremos click en _"Hacer público"_.
![image.png](/.attachments/image-39f53ff0-cfe2-4419-afa0-0519d46abde6.png)

Una vez hecho público, haremos click nuevamente en el checkbox, se desplegará el siguiente prompt, sobre el cual copiaremos la siguiente URL.
![image.png](/.attachments/image-ea482399-8728-445f-afcc-6880c1ecf1cc.png)

La forma de validar que la campaña/banner ya es público, es pegar la URL en un browser cualquiera, el cual debería mostrar el banner.
![image.png](/.attachments/image-38304494-8363-4aa8-a875-3943c6dedf4e.png)

###Carga de Campaña vía Postman
####Búsqueda por categoría
Para realizar una carga de campaña por "Búsqueda de Categoría", necesitaremos los siguientes datos:
- URL de banner desde S3.
- Nombre de Categoría.
- ID de Categoría.
- Fecha de vigencia de campaña (fecha inicio - fecha fin).

Para identificar la categoría y el ID necesitaremos ingresar a la base de datos en live y ejecutar la siguiente query.

`select catgroup_id,identifier,lastupdate from catgroup ;`

Esto nos dará el ID de la categoría.
![image.png](/.attachments/image-bc687727-455e-4f05-bb26-dc9fee4e4b0d.png)

Normalmente esto tendrá sentido con la url que nos envíen en el ticket.
![image.png](/.attachments/image-276b07d6-d62f-4633-a6de-04434dbbb09e.png)

El formato en el Body del JSON que ocuparemos para este caso será el siguiente:

```
[
{
"date_from": "Fecha Inicio",
"date_to": "Fecha Fin",
"image": "URL de IMAGEN",
"name": "Nombre de Campaña",
"order": 1,
"search": {
"id": "ID de Categoría",
"name": "Nombre de Categoría"
},
"type": "BC",
"scope": "kiosco"
}
]
```
_Nota: El campo "order" será por defecto_

- Tener en cuenta que type refiere al tipo de búsqueda: BC Búsqueda por Categoría | BT: Búsqueda por Término (Keyword).
- El campo scope puede variar en: kiosco - app.
- El campo date_from: Corresponde a la fecha inicio de la campaña.
- El campo date_to: Corresponde a la fecha fin de la campaña.
- El campo image: Corresponde a la URL completa del banner, desde el S3.
- El campo name: Corresponde al nombre de la campaña, también puede ser el nombre del banner.
- El campo term: Corresponde al keyword.
- El campo name: Corresponde al nombre de la Categoría.

Un ejemplo de JSON para cargar a Postman:


```
[
{
"date_from": "31/07/2019",
"date_to": "07/08/2019",
"image":
"https://kioskopublic.s3.us-east-2.amazonaws.com/TOD4782K-LED/led.png",
"name": "televisores-led",
"order": 1,
"search": {
"id": "10003",
"name": "televisores-led"
},
"type": "BC",
"scope": "kiosco"
}
]
```

Luego de tener el Body armado en el Postman, daremos click en _"Send"_.
![image.png](/.attachments/image-add3fe9b-7153-4585-b47b-045044f8e907.png)

Al ser cargado correctamente aparecerá el siguiente mensaje:
![image.png](/.attachments/image-94982928-e33c-4101-a6d6-a8078db593e7.png)

####Búsqueda por Término (Keyword)
Para realizar una carga de campaña por "Búsqueda de Categoría", necesitaremos los siguientes datos:
- URL de banner desde S3.
- Nombre de Display para el motor de búsqueda.
- Keyword.
- Fecha de vigencia de campaña (fecha inicio - fecha fin)

El formato en el Body del JSON es el siguiente.


```
[
{
"date_from": "Fecha Inicio",
"date_to": "Fecha Fin",
"image": "URL de IMAGEN",
"name": "Nombre Campaña",
"order": 1,
"search": {
"term": "KEYWORD",
"label": "Nombre Display"
},
"type": "BT",
"scope": "kiosco"
}
]
```

_Nota: El campo "order" será por defecto._

- Tener en cuenta que type refiere al tipo de búsqueda: BT: Búsqueda por Término (Keyword). | BC Búsqueda por Categoría
- El campo scope puede variar en: kiosco - app.
- El campo date_from: Corresponde a la fecha inicio de la campaña.
- El campo date_to: Corresponde a la fecha fin de la campaña.
- El campo image: Corresponde a la URL completa del banner, desde el S3.
- El campo name: Corresponde al nombre de la campaña, también puede ser el nombre del banner
- El campo term: Corresponde al keyword
- El campo label: Corresponde al nombre que Marketing o Comercial quieran que se vea cuando el banner redireccione a la url.

Un ejemplo de JSON para cargar a Postman:


```
[
{
"date_to": "fecha",
"date_from": "fecha",
"image":
"https://kioskopublic.s3.us-east-2.amazonaws.com/TOD4782K-Dormitorio/dor
mitorio.png",
"name": "Dormitorio",
"order": 1,
"search": {
"term": "kwowago",
"label": "Dormitorio"
},
"type": "BT",
"scope": "kiosco"
}
]
```

Luego de tener el Body armado en el Postman, daremos click en _"Send"_.
![image.png](/.attachments/image-b449a032-b4a5-483f-b6e2-64a74d5bffbd.png)

Al ser cargado correctamente aparecerá el siguiente mensaje:
![image.png](/.attachments/image-c43d8460-7813-4af9-ae87-5d51274ca120.png)

##Validación de Campaña - Emulación Kiosko

La primera validación se realizará en la base de datos de Kiosko, que la campaña haya sido correctamente cargada, con la siguiente query:

`select * from public.campaigns;`

![image.png](/.attachments/image-a44c1573-1734-43a6-8eec-c00b4c3fcee7.png)

Con esto validamos que la campaña ha sido cargada.
Si queremos asegurarnos de esto, deberíamos simular un kiosko, validar que el banner figura en el kiosko, hacer click y validar que la imagen redireccione a la categoría.

![image.png](/.attachments/image-5651cc90-bf75-4bea-b1c3-d0271be99af3.png)

![image.png](/.attachments/image-348359bc-77ca-437a-af13-06a5c888cd1d.png)

Para las campañas cargadas por Keyword, la validación por base de datos es la misma. La única diferencia en el simulador de Kiosko será que cuando el banner te redirija a la URL, debes validar el que el label figure en el display.
![image.png](/.attachments/image-a42c4c43-9649-4233-bde1-c87041f6a816.png)

![image.png](/.attachments/image-b3842f76-05a6-47b4-b3e2-b70020e6b013.png)

![image.png](/.attachments/image-d22134e1-7492-46d3-bf30-f9af631fe1d0.png)


