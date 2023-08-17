Historia: 
(Mencionar Historia con el simbolo "#" + el número de ticket.)

| Descripción | Título de la Canción |
|--|--|
[[_TOC_]]

----
#Compendio Técnico


_A continuación se informan los siguientes cambios realizados a nivel de Desarrollo._

----
##Desarrollo/QA
###I - Cambio 1
**FrontEnd:**
1. 
2. 
3. 

###I - Cambio 2
Comentarios
1. 
2. 
3. 

###I - Cambio 3
**Worker:**
1. 
2. 
3. 

----

#Documentación Operaciones
_A continuación se entregará información relevante de acuerdo a las modificaciones realizadas, correspondiente a la Operación y cómo Operar los nuevos cambios en producción. Vale decir: Diagramas de flujo asociados en caso de aplicar, validaciones a realizar en la Operación, tips de revisión, etc._

##Validación 1
Al realizar filtros se validarán los  siguientes cambios:

_Imagen 1_

Comentarios

_Imagen2_

--

###Validacón 2
*Worker*

_Imagen 1_

--

###Diagrama Explicativo (Ejemplo)
_Solo si aplica_

::: mermaid
 sequenceDiagram
    %%autonumber 
    participant 3 as Venta Efectiva
    participant tlog as TLOG
    participant sdd as SDD
    participant bm as BM
    participant r1 as Retail 1
    participant r2 as Retail 2
    participant jde as JDE

        
   3 ->> tlog : genera xml
   tlog ->> sdd : tlog
   tlog ->> bm : tlog
   bm ->> r1 : tlog
   r1 ->> r2 : valida info
   r2 ->> jde : valida info

:::

--
###Tabla Explicativa (Ejemplo)
_Solo si aplica_

| Titulo 1 | Titulo 2 | Titulo 3 | Titulo 4 |
|--|--|--|--|
| A1 | B1 | C1 | D1 |
| A2 | B2 | C2 | D2 |
| A3 | B3 | C3 | D3 |

----

##Revisión Adicional (Ejemplo)

Una vez implementado en producción, adicional a la revisión visual en el FrontEnd, es posible visualizar los logs asociados al Front en los servidores de aplicaciones en las siguientes rutas:

_/home/ubuntu/.pm2/logs/abcdin-frontend-error-*.log
/home/ubuntu/.pm2/logs/abcdin-frontend-out-*.log_

Así también, es posible realizar la revisión vía pm2 dentro de los servidores de aplicación.
Usuario: ubuntu

- Comando _pm2 list_
- Luego _pm2 log abcdin-frontend_ ó _pm2 log "id de aplicación"_ 
![image.png](/.attachments/image-3b92c558-cdc9-419a-b9c9-36a7e7a08fae.png)


----
##Manual Técnico Paso a Producción
El Paso a Producción se estará llevando a cabo mediante el siguiente documento Técnico, en los servidores de Aplicación:

[Manual Tecnico Paso a Producción Front End](https://dev.azure.com/ADretail/kiosko/_wiki/wikis/kiosko.wiki/281/Manual-T%C3%A9cnico-Paso-a-Producci%C3%B3n-Front-End)

[Manual Tecnico Paso a Producción Back End](https://dev.azure.com/ADretail/kiosko/_wiki/wikis/kiosko.wiki/283/Manual-T%C3%A9cnico-Paso-a-Producci%C3%B3n-Back-End)
