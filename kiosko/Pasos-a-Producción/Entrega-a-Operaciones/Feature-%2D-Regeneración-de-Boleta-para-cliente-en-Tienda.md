Historia de usuario:
#69232

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Habilitar un endpoint para que se pueda obtener la boleta indicando un folio.

#Problema:
Actualmente cuando los clientes solicitan la boleta no hay un método simple para hacerlo. Por lo que se requiere poder regenerar la boleta.

#Solución:
se implementó nueva screen en kiosko para obtener la boleta, está disponible en la ruta:

www.url_kiosko.cl/ticket/{folio}

Esto habilita la siguiente pantalla donde se podrá descargar la boleta como PDF.

![image.png](/.attachments/image-9c7d2fe9-14ca-4e18-8bd0-f0bc236d00f2.png)


Este cambio involucró la creación de la screen en el front además de la creación del endpoint en backend, al que se puede acceder mediante esta url:

GET
url_backend_kiosko/voucher/{folio}

Lo que devuelve la siguiente respuesta:


```
{
    "ticket": "pdf_base_64"
}
```


#QA

