#Procedimiento e Implementación

_Procedimiento específico de Back-end._

----

[[_TOC_]]

----

##Observaciones

Todos los procedimientos deben ser realizados con el usuario Ubuntu.
Todos los comandos deben ser ejecutados dentro de las carpetas de los proyectos correspondiente

----
##Procedimiento de respaldo de rama estable
_Este procedimiento debe ser realizado en todos los servidores donde se realiza el deploy._

| Actividad | Comando |
|--|--|
| Entrar a la carpeta | _cd /opt/kiosko-back_  |
| Crear rama para el rebase | _git checkout -b rebase/25072020-1_ (Patron: rebase/ddmmyyy-nºIntento)|
| Realizar commit del rebase | _git add . && git commit -m_ “Initial commit rebase”|
| Subir los cambios al servidor | _git push --set-upstream origin rebase/example-rebase_ |

----
##Procedimiento de deploy

| Actividad | Comando |
|--|--|
| Entrar a la carpeta | _cd /opt/kiosko-back_ |
| Ir a la rama actual del proyecto | _git checkout -f mm-feature/development-add-field-iva-in-voucher_ |
| Descargar la versión actual del proyecto | _git pull_ |
| Instalar nuevas dependencias| _npm install_ |
| Actualizar el contenedor del aplicativo | _pm2 restart ${id aplicación}_ |

----
##Procedimiento de rollback (Back-end)

| Actividad | Comando |
|--|--|
| Detener aplicación | _pm2 stop ${id aplicación}_ |
| Bajar la aplicación | _pm2 delete ${Id aplicación}_ |
| Cambiar a la rama estable | _git checkout rebase/25072020-1 (Patron: rebase/ddmmyyy-nºIntento)_ |
| Descargar la version estable | _git pull_ |
| Inicia solo la aplicación de back-end  | _npm start_ |
| Verifica que la aplicación quedó levantada chequeando que exista un proceso llamado ‘abcdin-backend’ en el visor de pm2 | _pm2 list_ |

![image.png](/.attachments/image-bc3b2034-88ca-4031-b8b1-6b59df0a3bbe.png)