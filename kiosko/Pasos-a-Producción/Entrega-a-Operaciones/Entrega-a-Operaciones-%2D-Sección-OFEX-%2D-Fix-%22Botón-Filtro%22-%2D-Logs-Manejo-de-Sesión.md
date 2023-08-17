Historia: #4822 #4820

| Descripción | Modificaciones Front - Visual Filtros Ofex |
|--|--|
[[_TOC_]]

----
#Compendio Técnico


_A continuación se informan los siguientes cambios realizados a nivel de Desarrollo._

----
##Desarrollo/QA
###I - Botón filtro por Ofex
**FrontEnd:**
1. Agrego 2 archivos, para manejar por redux el tema del filtro, los archivos son src/store/ofex/api.js y src/store/ofex/ofex.js
2. Modifico archivo src/store/catalog/api.js, para hacer lógica de búsqueda según producto, categoría y ofex
3. Agrego botón de filtro en src/components/Catalog/index.js y le doy estilo en src/components/Catalog/Catalog.scss
4. En archivo src/components/Facet/index.js agrego props onlyOfex
5. En archivo src/store/reducer.js agrego el correspondiente a ofex

###II - Logs Manejo de Sesión

Se agregan logs a lo largo del proceso de venta de un producto, recorriendo cada archivo y sus métodos, mostrando los parámetros utilizados y sus respuestas.
Modificación de los siguientes componentes:

**• Archivo:** src/components/order/route.js
**• Método:** preparePayment
**• Logs:**
    log.info(`<<< ROUTE EXECUTED: /orders/:orderId/preparePayment >>>`);
    log.info(`<<< METHOD EXECUTED: preparePayment() in src/components/order/route.js >>>`);
    log.info(`<<< METHOD EXECUTED: preparePayment() in src/components/order/controller.js >>>`);
    log.info(`<<< - PARAMS SENT: >>>`);
    log.info(`<<< - ORDER: ${req.order} >>>`);
    log.info(`<<< - TOTEM: ${req.totem} >>>`);
    log.info(`<<< - CARDTYPE: ${req.body.cardType} >>>`);
    log.info(`<<< - INSTALMENTS: ${req.body.instalments} >>>`);
    log.info(`<<< - KIOSK: ${req.kiosk} >>>`);
    log.info(`<<< RESULT PREPARE PAYMENT: ${result} >>>`);
    log.info(`<<< ERROR PREPARE PAYMENT: ${err} >>>`);

**• Archivo:** src/components/order/route.js
**• Método:** orchestra
**• Logs:**
log.info(`<<< ROUTE EXECUTED: /orders/:orderId/orchestra >>>`);
log.info(`<<< METHOD EXECUTED: orchestra() in src/components/order/route.js >>>`);
log.info(`<<< METHOD EXECUTED: orchestra() in src/components/order/controller.js >>>`);
log.info(`<<< - PARAMS SENT: >>>`);
log.info(`<<< - ORDER: ${req.order} >>>`);
log.info(`<<< - TOTEM: ${req.totem} >>>`);
log.info(`<<< - PAYMENTFLOW: ${req.body.paymentFlow} >>>`);
log.info(`<<< - VTOL: ${req.body.vtol} >>>`);
log.info(`<<< RESULT ORCHESTRA: ${result} >>>`);
log.info(`<<< ERROR ORCHESTRA: ${err} >>>`);

**• Archivo:** src/components/order/controller.js
**• Método:** preparePayment
**• Logs:**
log.info(`<<< METHOD EXECUTED: getStock() in src/services/milliway/api/services.js >>>`);
log.info(`<<< - PARAMS USED: >>>`);
log.info(`<<< - ORDER: ${order} >>>`);
log.info(`<<< - ORDER PRODUCTS: ${order.order_products} >>>`);
log.info(`<<< - TOTEM: ${totem} >>>`);

**• Método:** preparePayment createOrderPayment
**• Logs:**
log.info(`<<< METHOD EXECUTED: preparePayment() -> createOrderPayment() in c/services/milliway/api/services.js >>>`);
log.info(`<<< CREATE TRANSACTION >>>`);
**TRY**
log.info(`<<< IF THERE IS A PAYMENT ORDER >>>`);
log.info(`<<< CARD TYPE === ABC >>>`);
log.info(`<<< CARD TYPE !== ABC >>>`);
log.info(`<<< DELETE AND CREATE PAYMENT FOR TRANSBANK >>>`);
log.info(`<<< IF THERE IS NO PAYMENT ORDER >>>`);
log.info(`<<< CREATE PAYMENT FOR TRANSBANK >>>`);
**CATCH**
log.error(`[order][controller][preparePayment][createOrderPayment][Error]: ${err} - [transaction rollback]`);

**• Método:** preparePayment updateOrder
**• Logs:**
log.info(`<<< METHOD EXECUTED: preparePayment() -> updateOrder() in src/services/milliway/api/services.js >>>`);
log.info(`<<< CREATE TRANSACTION >>>`);
**TRY**
log.info(`<<< IF ALL PRODUCTS HAVE STOCK >>>`);
log.info(`<<< IF ALL PRODUCTS NOT HAVE STOCK >>>`)
**CATCH**
log.error(`[order][controller][preparePayment][updateOrder][Error]: ${err} - [transaction rollback]`);

**• Archivo:** src/components/order/controller.js
**• Método:** orchestra
**• Logs:**
**TRY**
log.info(`<<< UPDATE STATUS ORDER (when user is in checkout process and orchestra) >>>`);
log.info(`<<< UPDATE STATUS ORDER (when orchestra finished) >>>`);
**CATCH**
log.error(`[order][controller][orchestra][Error]: ${err}`);

**• Archivo:** src/components/order/controller.js
**• Método:** orchestra
**• Logs:**
log.info(`<<< METHOD EXECUTED: getStock -> getStockFormatter in src/services/milliway/api/services.js >>>
 <<< RESULT: ${_formattedData} >>>`);
log.info(`<<< METHOD EXECUTED: getStock -> socketData in src/services/milliway/api/services.js >>>
 <<< RESULT: ${_netRespond} >>>`);
log.info(`<<< METHOD EXECUTED: getStock -> xmlToJson in src/services/milliway/api/services.js >>>
 <<< RESULT: ${JSON.stringify(_formattedResponse, null, 2)} >>>`);
log.info(`<<< RESPONSE: ${JSON.stringify(manageResponseGetStock(_formattedResponse), null, 2)} >>>`);

**• Archivo:** src/components/orquestador/index.js
**• Método:** init
**• Logs:**
log.info(`<<< METHOD EXECUTED: init() in src/components/orquestador/index.js >>>`);
log.info(`<<< - PARAMS USED: >>>`);
log.info(`<<< - ORDER: ${order} >>>`);
log.info(`<<< - TOTEM: ${totem} >>>`);
log.info(`<<< - PAYMENTFLOW: ${paymentFlow} >>>`);
log.info(`<<< - VTOL: ${vtol} >>>`);
**TRY**
log.info(`<<< METHOD EXECUTED:
init() -> _prepareServices(_getSelectedServices()) in src/components/orquestador/index.js>>>`);
log.info(`<<< SELECTED AND PREPARE SERVICE >>>`);
log.error('Orchestra: index : Orchestra Canceled: ', JSON.stringify(_store.cancel, 4, 4));
log.info('Orchestra: index : FINISH ALL calls for order with folio: ', order.get('folio'));
log.info(`<<< RESULT PROCESS DATA: ${_processData(ticketOutput, vtol, warrantiesTicket, order)} >>>`);
**CATCH**
log.error('[orchestra][final] :', error);

**• Método:** init _initConfig
**• Logs:**
log.info(`<<< METHOD EXECUTED: init() -> _initConfig() in src/components/orquestador/index.js >>>`);
log.info(`<<< STORE OBJECT CONFIGURATION AND UPDATE order.on_us, order.order_payment.vtoltxr_id >>>`);

**• Método:** init _construct
**• Logs:**
log.info(`<<< METHOD EXECUTED: _construct() in src/components/orquestador/index.js >>>`);
log.info(`<<< UPDATE order.authorization_date >>>`);
log.info(`<<< UPDATE order.session_id >>>`);
**TRY**
log.info(`<<< IF SERVICE IS STAIN >>>`);
log.info(`<<< IF SERVICE IS CONFIRMSTOCK >>>`);
log.info(`<<< IF SERVICE IS QUOTA RESERVATION >>>`);
log.info(`<<< IF SERVICE IS CREATE CIC >>>`);
log.info(`<<< IF SERVICE IS CONFIRM FOLIO >>>`);
log.info('[FINISHED] confirmFolio');
**CATCH**
log.info(`<<< IF ERROR IN ANY SERVICE >>>`);
log.error(`Orchestra: Error in ${service.name} canceling reserve`);
log.error(`Orchestra: error: ${JSON.stringify(error.message)}`);

**• Método:** init _ticket.generate
**• Logs:**
log.info(`<<< METHOD EXECUTED: init() -> ticket.generate() in src/components/orquestador/index.js >>>`);
log.info(`<<< FORMAT AND GENERATE TICKET FILE >>>`);
log.info(`[ORCHESTRA][TICKET] Generating ticket with ${order.get("folio")}`);
**TRY**
**CATCH**
log.error("[ORCHESTRA][TICKET] Error generating boleta: ", error);

**• Método:** init generateWarrantyTicket
**• Logs:**
log.info(`<<< METHOD EXECUTED: init() -> ticket.generateWarrantyTicket() in src/components/orquestador/index.js >>>`);
log.info(`<<< FORMAT TICKET WARRANTY >>>`);


----

#Documentación Operaciones
_A continuación se entregará información relevante de acuerdo a las modificaciones realizadas, correspondiente a la Operación como tal. Vale decir: Diagramas de flujo asociados en caso de aplicar, validaciones a realizar en la Operación, tips de revisión, etc._

##Cambios FrontEnd
Al realizar filtros se validarán los  siguientes cambios:

Al buscar por Producto:

![image.png](/.attachments/image-3cdadc01-64ac-4ecd-b383-729a0e770d72.png)

--

Al seleccionar "Ver Ofertas Exclusivas":

![image.png](/.attachments/image-184349ae-cd1e-409a-a9a3-0bc4cd6a5d89.png)

--

Al buscar por categoría:

![image.png](/.attachments/image-f491a561-f386-4230-a3cc-a2dc2e1cd410.png)

##Cambios BackEnd
- No aplica

##LOGS

Se agregaron los siguientes logs que son posibles visualizarlos asociados a el bakend
En los servidores de aplicaciones en la siguiente 
ruta/home/ubuntu/.pm2/logs/abcdin-backend-aut-43.log 
ruta/home/ubuntu/.pm2/logs/abcdin-backend-error-43.log

Así también, es posible realizar la revisión vía pm2 dentro de los servidores de aplicación.
Usuario: ubuntu 
-	Comando: cd opt/kiosko-back
-	Luego: /pm2 log
 ![log.png](/.attachments/log-f36eaf23-f830-4569-8338-9266d3a7300f.png)

----

##Revisión Adicional

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
