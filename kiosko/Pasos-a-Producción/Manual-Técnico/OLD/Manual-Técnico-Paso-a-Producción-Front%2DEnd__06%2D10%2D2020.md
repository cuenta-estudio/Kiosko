#Procedimiento e Implementación

_Procedimiento específico de Front-end._

----

[[_TOC_]]

----

##Observaciones

Todos los procedimiento deben ser realizados con el usuario Ubuntu.
Todos los comandos deben ser ejecutados dentro de las carpetas de los proyectos correspondientes

-	Antes de mergear develop a master, realizar un respaldo de la rama ‘master’ para esto ir a la tabla ‘Procedimiento de respaldo de rama master
-	Para el procedimiento normal de deploy seguir con la tabla ‘Procedimiento de deploy’


----
##Procedimiento de respaldo de rama estable
_Este procedimiento debe ser realizado en todos los servidores donde se realiza el deploy._

| Actividad | Comando |
|--|--|
| Entrar a la carpeta | _cd /opt/kiosko-front_  |
|  Descartar cambios realizados en el proyecto de forma local | _git checkout ._ |
| Cambiar a la rama develop | git checkout master |
| Verificar que se está bajo la rama ‘develop’ | git branch |
| Crear una rama de respaldo para el rollback | git checkout -b spike-master/feature/EX-87-maintenanceScreen |
| | |
| | |


----
##Procedimiento de deploy

| Actividad | Comando |
|--|--|
| Hacer merge de develop a master desde la consola | |
| Ingresar a la carpeta del proyecto | _cd /opt/kiosko-front_ |
| Descartar cambios realizados en el proyecto de forma local | _git checkout ._ |
| Cambiar a la rama master | _git checkout master_ |
| Verificar que se está bajo la rama ‘master’ | _git branch_ |
| Sincronizar el estado local con las nuevas actualizaciones del repositorio | _git fetch origin_ |
| Descargar los nuevos cambios que existan en la rama | _git pull --rebase_ |
| instalar nuevas dependencias | _npm install_ |
| Construye los archivos de estilos necesarios | _npm run build-css_ |
| Construye los archivos de código necesarios | n_pm run build_ |
| Obtener el id de la aplicación ‘abcdin-frontend’  para poder detenerla. Esta se encuentra bajo la columna ‘id’ | _pm2 list_ |
| Bajar la aplicación | _pm2 delete ${Id aplicación}_ |
| Se levanta el proyecto bajo el gestor de aplicaciones pm2. | _pm2 serve build 3000 --name abcdin-frontend_ |
| Verifica que la aplicación quedó levantada chequeando que exista un proceso llamado ‘abcdin-frontend’ en el visor de pm2. | _pm2 list_ |

----
##Procedimiento de rollback (Front-end)

| Actividad | Comando |
|--|--|
| Detener aplicación | _pm2 stop ${id aplicación}_ |
| Bajar la aplicación | _pm2 delete ${Id aplicación}_ |
| Cambiar a la rama estable | _git checkout spike-master/feature/EX-87-maintenanceScreen_ |
| Construye los archivos de estilos necesarios | _npm run build-css_ |
| Construye los archivos de código necesarios | _npm run build_ |
| Se inicia aplicación | _pm2 serve build 3000 --name abcdin-frontend_ |
| Verifica que la aplicación quedó levantada chequeando que exista un proceso llamado ‘abcdin-backend’ en el visor de pm2 | _pm2 list_ |

![image.png](/.attachments/image-bc3b2034-88ca-4031-b8b1-6b59df0a3bbe.png)