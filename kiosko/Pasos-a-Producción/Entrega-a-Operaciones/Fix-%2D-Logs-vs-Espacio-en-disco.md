Historia de usuario:
#41792

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Deshabilitar la escritura de logs desde el proyecto, ya que generan duplicados generando que el disco del servidor se llene más rápido de lo normal. Estos logs no se utilizan, ya que se utilizan otras herramientas para ello.

#Problema:
Se realizó el análisis del caso y los logs eran generados por la librería de logs de la aplicación, ya que en su configuración se especificaba almacenar logs en una carpeta. Esto provocaba que rápidamente se llenara el disco del servidor.

#Solución:
Se eliminó de la configuración de la librería "winston" las instrucciones para almacenar los logs. Con esto ya no se genera el archivo de logs dentro del proyecto.



QA


En la siguiente imagen podemos visualizar que ya no existen logs basura:

![logs wiki 1.png](/.attachments/logs%20wiki%201-8358e8a7-96ab-4417-8237-1b1998dbfff2.png)