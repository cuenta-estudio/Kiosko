Historia: 
#29903

Autor: Camilo Alaniz


[[_TOC_]]

----
#Desarrollo
##Objetivo
El principal objetivo de este procedimiento es realizar un fix a un problema encontrado durante las pruebas del motor promo.

##Problema:
Se reportó a desarrollo un problema con el motor promo que se estaba utilizando, puesto que siempre se utilizaba el antiguo, pero debería de utilizarse el nuevo o el antiguo dependiendo de una variable en base de datos .

Esto no estaba ocurriendo, backend no estaba enviando el tag correspondiente y estaba ignorando la variable de base de datos de la tabla kiosks columna "new_promo". 

Se realizó el análisis siguiendo la traza de datos, y se determinó que el problema es que no está mapeada dicha variable en el esquema del orm en el backend, por lo que se envía siempre como undefined, al verificar qué motor se debe utilizar siempre cae en falso debido a ese undefined.

##Solución:
La solución fue añadir la variable faltante al esquema "kiosks" que está ubicado en src/components/kiosks/model.js. 

`new_promo: {
        type: DataTypes.BOOLEAN,
        allowNull: false,
        defaultValue: true,
      },`

Esto permite al ORM dar el valor correspondiente a dicha variable, lo que permite a la aplicación determinar correctamente qué motor debe utilizar.

----
#QA


Para aplicar este cambio es necesario cambiar la tabla kiosks, se busca la tienda en la que se requiere probar y se activa(true) el nuevo motor promo (new_promo) y esto se visualiza de la siguiente manera
![2021-04-01 12_38_37-pgAdmin 4.png](/.attachments/2021-04-01%2012_38_37-pgAdmin%204-0c438375-e075-4f65-b6a1-da0dc3fdd9e1.png)


Y este cambio nos da la siguiente respuesta![imagen promo 2.png](/.attachments/imagen%20promo%202-c33e755e-9464-4cce-9f83-400ac84a77ca.png)












