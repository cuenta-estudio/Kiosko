Historia de usuario:
#35920

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Corregir problema que ocurre con las sesiones de VTOL, ya que provoca que no se completen todos los flujos de la compra, por lo que la venta no llega hasta backoffice, generando inconsistencia y problemas contables.

#Problema:
Bajo el análisis en conjunto con el proveedor de VTOL se determinó anteriormente que el problema estaba en la librería "vtol-bridge" que comunica el Kiosko con la librería de VTOL. Por lo que se debía analizar y corregir dicha funcionalidad en la librería.

Se revisó dicha librería "vtol-bridge" y el problema proviene de el evento "originalsale" de vtol que se ejecuta cuando la venta fue aprobada y pagada, ya que ésta librería intermedia indicaba a VTOL un cierre de sesión antes de tener una abierta, por lo que generaba inconsistencia en su funcionamiento.

#Solución:
Se eliminaron las instrucciones de cierre de sesión al inicio de esa función, ya que no deben estar ahí. Esto se realizó dentro de la librería intermedia "vtol-bridge" y compilada para generar un nuevo ejecutable. El cambio se aplica simplemente reemplazando el archivo en el Kiosko correspondiente.

#Despliegue:
Como este cambio involucra únicamente la librería intermedia "vtol-bridge", no es necesario realizar un despliegue del backend o frontend. Por lo que se debe de realizar una instalación individual y manual por cada Kiosko siguiendo las siguientes instrucciones:

Antes de comenzar, se debe ubicar la carpeta donde actualmente el kiosko tiene instalada la librería "vtol-bridge", debería encontrarse en la siguiente ruta del directorio principal del Kiosko "KIOSKO/lib/KIOSKO/VTOL". Este será el directorio sobre el que trabajaremos.


Esta carpeta tendrá dentro, una carpeta llamada vtol-bridge-flow, la cual llamaremos "versión A", que contiene unos archivos de configuración que utilizaremos.


***
**_IMPORTANTE: Realizar una copia de esta carpeta como respaldo._**
***


Pasos:

1- Se enviará una copia de esta carpeta, con la nueva versión de la librería (versión B), la cual ya está prácticamente lista para su funcionamiento. Pero es importante no reemplazar aún ya que debemos copiar algunos archivos de configuración importantes.

2- Dirigirse a la carpeta "bin" ubicada dentro de la versión A, y copiar el archivo llamado "config.properties" (puede que solo aparezca como "config", su extensión es "properties").
3- Dirigirse a la carpeta "bin" ubicada dentro de la versión B, y reemplazar el archivo de config por el que acabamos de copiar (config.properties version A).

Básicamente, se debe reemplazar la carpeta de dicha librería, pero mantener el archivo config.properties ya que este tiene los valores que utiliza cada Kiosko de forma particular e individual.

#QA


Luego de realizar los cambios podemos visualizar los logs de la siguiente manera:

![imagen 1.png](/.attachments/imagen%201-d5b3b889-21bb-467e-b13f-b4bd0114d2c7.png)

Se puede visualizar que cierra la sesión y luego abre una nueva... 



Por otra parte también podemos visualizar cuando 

   Genera la boleta electrónica: 
![imagen 3.png](/.attachments/imagen%203-97fe0ccb-7029-418e-8631-decc6cab61a5.png)


Generar el tlog:
![imagen 2.png](/.attachments/imagen%202-2a1f7458-b535-4b1f-ad13-90758ab29678.png)


Regenerar el tlog: 
![imagen 4.png](/.attachments/imagen%204-ddcc3715-5980-4db8-a36c-d909985f6699.png)

Boleta electrónica: 
![imagen 5.png](/.attachments/imagen%205-ecdab5e8-9f87-437a-ad66-01bd0a07718a.png)