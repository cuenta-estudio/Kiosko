Historia: 
#223

| Descripción | Registrar en la BD cuando una venta es reversada |
|--|--|
[[_TOC_]]

----
#Compendio Técnico

A continuación se informan los cambios realizados a nivel de Desarrollo.

----

##Contexto
_Desarrollo que contempla el registro en Base de Datos de estado Nº 4 (Cancelado) y estado Nº 5 (Cancelado con error) al momento de realizar una venta. Es necesario destacar que el desarrollo original no contempló dichos estados, al parecer se asumía que toda transacción terminaría correctamente, por lo que toda venta finalizaba con estado Nº 3 (Pagado con éxito)_ 

----

##Desarrollo
###I - Cambio - Registro estado Nº 4
**FrontEnd:**
1. Se intervienen los siguientes archivos:
   - /src/components/Payment/index.js
   - /src/store/pinpad/pinpad.js
2. Si al momento de realizar el pago, la operación se cae ya sea por error del pinpad, cancelación voluntaria por medio del botón CANCELAR del pinpad, cancelación por TIMEOUT, error de lectura de tarjeta, etc. la aplicación ejecuta el nuevo endpoint creado en el backend desde el archivo /src/store/pinpad/pinpad.js registrando el estado Nº 4 en Base de Datos.

###I - Cambio  - Registro estado Nº 4
**Backend**
1. Se crea nuevo endpoint el cual permite la interacción con la Base de Datos.
2. El nuevo endpoint es PUT orders/:orderId/pinpadError
3. Se intervienen los siguientes archivos:
   - /src/components/order/controller.js
   - /src/components/order/index.js
   - /src/components/order/route.js
   - /src/middlewares/order/middleware.js

###II - Cambio  - Registro estado Nº 5
**Backend**
1. Toda venta al momento de realizar el pago, ejecuta una serie de servicios externos según el medio de pago seleccionado, si uno de estos servicios no responde correctamente, se aplica la REVERSA registrando el estado Nº 5 en Base de Datos.
2. Originalmente no se evaluaba si todos los servicio respondían correctamente, por lo que si esto sucedía, de igual forma en la operación se registraba el estado Nº 3, en este desarrollo esa condición es evaluada, registrando correctamente el estado que corresponde.
3. Se intervienen los siguientes archivos:
   - /src/components/order/controller.js
   - /src/components/orquestador/index.js


----
#Documentación Operaciones
_A continuación se entregará información relevante de acuerdo a las modificaciones realizadas, correspondiente a la Operación y cómo Operar los nuevos cambios en producción. Vale decir: Diagramas de flujo asociados en caso de aplicar, validaciones a realizar, tips de revisión y pruebas funcionales._

##QA 

Estado 4 = Cancelado: este se puede replicar luego del flujo de venta normal en el momento que en el que el pinpad aparezca  monto a cancelar se preciona botón ROJO (cancel) y se visualiza de esta manera en la BBDD.

![Screenshot-2020-12-16T18-58-00.741Z.png](/.attachments/Screenshot-2020-12-16T18-58-00.741Z-b6bc0b55-0359-46b2-a460-7b8892f03a0c.png)


Estado 5 = Cancelado con error: es un estado que se da cuando se presenta un error en un servicio y esto se visualiza de la síguiente manera. 

![Screenshot-2020-12-16T20-22-08.705Z.png](/.attachments/Screenshot-2020-12-16T20-22-08.705Z-6d5fe323-c951-41e0-9a88-38ff8f974d1f.png)

![Screenshot-2020-12-16T20-23-41.991Z.png](/.attachments/Screenshot-2020-12-16T20-23-41.991Z-9c18359d-ef5d-4e53-b495-e63783d472df.png)

![Screenshot-2020-12-16T20-23-16.549Z.png](/.attachments/Screenshot-2020-12-16T20-23-16.549Z-be95661a-4863-4d6f-a26c-a894932397ca.png)




