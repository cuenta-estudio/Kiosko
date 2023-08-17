Historia de usuario:
#61586

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Actualizar la librería Log4j de la aplicación vtol-bridge.

#Problema:
Se ha informado recientemente una vulnerabilidad crítica de la librería Log4j de Java, librería que es utilizada por la aplicación vtol-bridge de Kiosko.

#Solución:
Se evaluó el problema de vulnerabilidad informado, pero se ha determinado que no afecta a Kiosko ya que se utiliza una versión más antigua de la librería que se ha informado no tiene dicha brecha, pero si otras vulnerabilidades menores que ya no tienen soporte en dicha versión. 

Por lo tanto, se ha decidido actualizar la librería Log4j para estar al día con la versión actual ya que estas vulnerabilidades ya no están presentes y tiene el soporte al día.

Se realizó también el cambio al código correspondiente de la librería de vtol-bridge, ya que en el upgrade de versión, cambió la interfaz de la librería por lo que se debió implementar correcciones menores.

El cambio de versiones fue el siguiente:
Antes: Log4j v1.2.17
Actual: Log4j v2.16.0

Este fix, tuvo impactos a nivel de configuración, lo que será detallado en la sección Instalación.

#Instalación:
La instalación de la nueva versión de la librería es la misma que en anteriores oportunidades, pero añadiendo un par de pasos extra. 
Se proporcionará un .rar con los archivos:

- vtol-bridge-flow-1.0.0-SNAPSHOT.jar
- log4j2.properties
- vtol-bridge-flow.bat

Pasos para la instalación:

1.- Crear un respaldo de la actual carpeta de vtol que posea el kiosko

2.- Al igual que siempre, se debe copiar y reemplazar el archivo vtol-bridge-flow-1.0.0-SNAPSHOT.jar dentro de la carpeta "lib" ubicada en "C:\KIOSKO\lib\KIOSKO\VTOL\vtol-bridge-flow-1.0.0\lib\"

** Nuevos pasos **

3.- Copiar el archivo log4j2.properties dentro de la carpeta "bin" ubicada en "C:\KIOSKO\lib\KIOSKO\VTOL\vtol-bridge-flow-1.0.0\bin\", dicha carpeta debería contener ahora un archivo log4j.properties que es el antiguo y el nuevo log4j2.properties que es el que acaba de copiar. Esta versión de la librería deja de utilizar el archivo log4j.properties y pasa a utilizar el nuevo, si lo abres, podrás ver que contiene la configuración del formato de los logs, por lo que puedes dejarlo así tal cual se envía. El antiguo archivo log4j.properties puedes eliminarlo, ya no será utilizado por la aplicación.

4.- Ahora que se ha cambiado el archivo de configuración, hay que indicarle al ejecutable que debe leer dicho archivo, por lo que hay que copiar y reemplazar el archivo vtol-bridge-flow.bat que está dentro de la misma carpeta bin. Este nuevo archivo lee la configuración desde el nuevo log4j2.properties, por lo que es importante cambiarlo para que funcione sino no será capaz de encontrarlo.

5.- Listo, ya puedes probar. La librería debería de seguir funcionando al igual como lo hacía, pero ahora la salida de logs se realiza en una nueva carpeta llamada "logs" que está dentro de la misma carpeta bin.

#QA 

Luego de realizar la actualización de la librería se realizaron pruebas de compras en kisoco con flujos de compras completas validando así que dicho fix no afecta el funcionamiento del kiosco, dejando como evidencia la siguiente boleta de compra en kiosco:

![Boleta .png](/.attachments/Boleta%20-ff23b055-07d7-4e41-8694-0b699f6334a5.png)


Por otra parte también podemos visualizar como se genera correctamente el Tlog:

![tlog 1 .png](/.attachments/tlog%201%20-20b8f503-15ad-40c7-a479-ed96f992c965.png)![tlog 2.png](/.attachments/tlog%202-81c85b85-7909-4720-a726-a290e0443444.png)![tlog 3.png](/.attachments/tlog%203-381b23c0-9ddd-4c7b-a842-5f3c691d69b8.png)


