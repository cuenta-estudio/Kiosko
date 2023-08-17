#Procedimiento e Implementación

_Procedimiento específico de Back-end._

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
| Entrar a la carpeta | _cd /kiosko_back_  |
|  Descartar cambios realizados en el proyecto de forma local | _git checkout ._ |
| Cambiar a la rama master | git checkout master |
| Verificar que se está bajo la rama ‘master’ | git branch ![image.png](/.attachments/image-8c36ab38-8aeb-4369-93ed-a4ff5c6b929b.png) |
| Crear una rama de respaldo para el rollback | git checkout -b spike-master/feature/EX-87-maintenanceScreen |
| | |
| | |


----
##Procedimiento de deploy

| Actividad | Comando |
|--|--|
| Hacer merge de development a master desde la consola de aws | |
| Ingresar a la carpeta del proyecto | _cd /kiosko_back_ |
| Obtener el id de la aplicación ‘abcdin-backend’  para poder detenerla. Esta se encuentra bajo la columna ‘id’ | pm2 list ![image.png](/.attachments/image-c96b71d3-a120-4e90-84e6-88d36c7e00e4.png)
| Detener aplicación | pm2 stop ${id aplicación} |
| Bajar la aplicación| pm2 delete ${Id aplicación} |
| Descartar cambios realizados en el proyecto de forma local | _git checkout ._ |
| Cambiar a la rama master | _git checkout master_ |
| Verificar que se está bajo la rama ‘master’ | _git branch_ ![image.png](/.attachments/image-205a6753-facf-41ce-bca2-136132655829.png) | 
| Sincronizar el estado local con las nuevas actualizaciones del repositorio | _git fetch origin_  ![image.png](/.attachments/image-95da12cc-acfe-482e-8922-ca8f4a87fa6a.png)|
| Descargar los nuevos cambios que existan en la rama | _git pull --rebase_ |
| instalar nuevas dependencias | _npm install --production_ |
| Ejecutar migraciones | _sequelize db:migrate_ |
| Inicia solo la aplicación de back-end | ONLY_WEBSERVICE=true npm start_ |
| Verifica que la aplicación quedó levantada chequeando que exista un proceso llamado ‘abcdin-backend’ en el visor de pm2. | _pm2 list_ ![image.png](/.attachments/image-9626fb98-cacc-4649-97ca-26d9fb691584.png) |


----
##Procedimiento de rollback (Back-end)

| Actividad | Comando |
|--|--|
| Deshacer migración | _sequelize db:migrate:undo --name 20190508121750-addColumnOpenToKiosk.js_ |
| Detener aplicación | _pm2 stop ${id aplicación}_ |
| Bajar la aplicación | _pm2 delete ${Id aplicación}_ |
| Cambiar a la rama estable | _git checkout spike-master/feature/EX-87-maintenanceScreen_ |
| Inicia solo la aplicación de back-end  | _ONLY_WEBSERVICE=true npm start_ |
| Verifica que la aplicación quedó levantada chequeando que exista un proceso llamado ‘abcdin-backend’ en el visor de pm2. | _pm2 list_ ![image.png](/.attachments/image-2aacb480-6262-4f69-8066-a9e33e177f39.png) |
