Se adjuntarán a continuación una serie de comandos, los cuales aplican para reiniciar los servicios de aplicación en Kiosko.

[[_TOC_]]

#Introducción - Ruta Raíz

Para el inicio o el reinicio de cada servicio, debemos ir primero a la ruta raíz de este.
Esto lo realizamos de la siguiente manera:

Ingresamos al servidor y nos cambiamos al usuario ubuntu.

![image.png](/.attachments/image-2a741420-2708-4f57-82e5-b87082193dcd.png)

Podemos ver los servicios activos con el comando `pm2 list`
![image.png](/.attachments/image-7c78c8e7-b892-4c6e-9f58-772eca692e14.png)

Ahora dependiendo del servicio que queramos reiniciar ejecutamos el comando `pm2 show "servicio"` o `pm2 show "id"`
Esto nos mostrará una serie de datos correspondientes al servicio. Nosotros ocuparemos el "repository root". En caso de que no aparezca, también puede aplicar el "exec cwd". Siempre considerar el repository root inicialmente.
![image.png](/.attachments/image-dbc66393-8a1a-429b-b0b7-409437a54786.png)

En esa ruta ejecutaremos el inicio o reinicio de cada servicio.
_Nota: Esta ruta puede cambiar en el tiempo, no necesariamente será la misma ruta siempre. Además, para el caso de los dos servidores de aplicación, siempre tendrán las mismas rutas._

Se indicará la ruta raíz a la fecha que se realizó este documento, el cual podría cambiar en el futuro.

_Nota: el comando que inicia el servicio aplica para reinicio o para el inicio del mismo._

#App Servers

##Restart de Backend 


pm2 list
pm2 restart  abcdin-backend
pm2 list

##Bajada y Subida de Backend

pm2 list
cd /home/ubuntu/myagent/_work/r1/a/release-kiosko/s
 pm2 stop abcdin-backend
 pm2 delete abcdin-backend
 ONLY_WEBSERVICE=true npm start
 pm2 list

----


 ##Restart de Frontend
 
pm2 list
pm2 restart  abcdin-frontend
pm2 list

##Bajada y Subida de Frontend

pm2 list
 cd /opt/kiosko-front
 pm2 stop abcdin-frontend
 pm2 delete abcdin-frontend
 pm2 serve build 3000 --name abcdin-frontend
 pm2 list

----

##Restart Promo Service

pm2 list
pm2 restart promo-service
pm2 list

##Bajada y Subida de Promo Service

pm2 list
cd /home/ubuntu/myagent/_work/r2/a/release-kioskopromo/s
pm2 stop  promo-service
pm2 delete  promo-service
npm start
pm2 list

----
#Worker

##Restart Price Worker Service 

pm2 list
pm2 restart abcdin-price-worker
pm2 list

##Bajada y Subida de Worker Service

cd /opt/ebusiness_devops_kiosko_backendcloud_workers
pm2 list
pm2 stop abcdin-price-worker
pm2 delete abcdin-price-worker
npm start
pm2 list

##Restart Cache Worker Service 

pm2 list
pm2 restart abcdin-cache-worker
pm2 list

##Bajada y Subida de Cache Worker

cd /opt/ebusiness_devops_kiosko_cache_worker
pm2 list
pm2 stop abcdin-price-worker
pm2 delete abcdin-price-worker
npm start
pm2 list
