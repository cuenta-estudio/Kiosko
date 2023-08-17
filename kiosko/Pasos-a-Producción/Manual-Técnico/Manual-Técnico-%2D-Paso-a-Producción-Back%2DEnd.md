#Procedimiento e Implementación

_Procedimiento específico de Back-end._

----

[[_TOC_]]

----
##Observaciones

Todos los procedimientos deben ser realizados con el usuario Ubuntu.
Todos los comandos deben ser ejecutados dentro del directorio del proyecto correspondiente.

----
##Procedimiento de Deploy
_Este procedimiento debe ser realizado en todos los servidores donde se realiza el deploy._

| Actividad | Comando |
|--|--|
| Entrar al directorio del proyecto| _cd /opt/kiosko-back_  |
| Validar en qué rama nos encontramos | _git status_|
| Cambiar a la rama "Release" | _git checkout release_|
| Validar en qué rama nos encontramos | _git status_|
| Bajar los cambios actualizados de la rama al servidor local | _git pull_ |
| Instalar nuevas dependencias | _npm install --production_ |
| Ejecutar Migraciones (Solo si Aplica) | _sequelize db:migrate_ |
| Obtener el id de la aplicación ‘abcdin-backend’ para poder detenerla. Esta se encuentra bajo la columna ‘id’ | _pm2 list_ |
| Detener la aplicación | _pm2 stop ${Id aplicación}_ |
| Bajar la aplicación | _pm2 delete ${Id aplicación}_ |
| Se levanta el proyecto bajo el gestor de aplicaciones pm2 | _ONLY_WEBSERVICE=true npm start_ |
| Verifica que la aplicación quedó levantada chequeando que exista un proceso llamado ‘abcdin-backend’ en el visor de pm2 | _pm2 list_ |
----
##Procedimiento de Rollback

| Actividad | Comando |
|--|--|
| Validar estar en el directorio del proyecto| _cd /opt/kiosko-front_  |
| Validar en qué rama nos encontramos | _git status_|
| Cambiar a la rama "Master" | _git checkout master_|
| Validar en qué rama nos encontramos | _git status_|
| Instalar nuevas dependencias (rama master no presenta cambios, por lo tanto no es necesario el pull)| _npm install_ |
| Construye los archivos de estilos necesarios | _npm run build-css_ |
| Construye los archivos de código necesarios | _npm rum build_ |
| Obtener el id de la aplicación ‘abcdin-frontend’ para poder detenerla. Esta se encuentra bajo la columna ‘id’ | _pm2 list_ |
| Bajar la aplicación | _pm2 delete ${Id aplicación}_ |
| Detener la aplicación | _pm2 stop ${Id aplicación}_ |
| Se levanta el proyecto bajo el gestor de aplicaciones pm2 | _pm2 serve build 3000 --name abcdin-frontend_ |
| Verifica que la aplicación quedó levantada chequeando que exista un proceso llamado ‘abcdin-frontend’ en el visor de pm2 | _pm2 list_ |