Logs Adjuntos y Archivos de Conf:
[Kioskos con Problemas.rar](/.attachments/Kioskos%20con%20Problemas-b3c67ab2-1f03-4c11-9b1c-9a9b5ab316dc.rar)

#KAS_Ancud_092  -  192.2.92.244
Ultima Venta ABC: 11 Abril | Ultima Venta Webpay: 24 de Enero

##Errores Detectado en VTOL Bridge
```
2022-04-19 13:58:04 INFO  VtolClient:339 - closeSession :1110:0
1010:1650387478110
1028:Ok
1027:000
2:90
1:092

2022-04-19 13:58:04 ERROR Server:127 - El sistema se encuentra fuera de servicio para SOLKEYTRK o RECTRACK2
java.lang.Exception: El sistema se encuentra fuera de servicio para SOLKEYTRK o RECTRACK2
    at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:533) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
    at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
    at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
    at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
    at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
    at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-04-19 13:58:04 INFO  Server:56 - onMessage : org.java_websocket.WebSocketImpl@7c059f88: {​​"type":"reject"}​​
2022-04-19 13:58:04 INFO  Server:101 - reject
2022-04-19 13:58:05 INFO  VtolClient:289 - ****** checkResponseCode :1110:0
1010:1650387478110
1028:Ok
1027:000
2:90
1:092
```

##Errores Detectado en Vtol Client
```
2022-04-19 13:58:00,076 INFO  [PinpadMessageInterpreter] [Thread-3] GLOSA_CONFIRMAR_MONT : 3 cuotas 29494
2022-04-19 13:58:00,076 INFO  [PinpadMessageInterpreter] [Thread-3] GLOSA_CONFIRMAR_MONT : 
2022-04-19 13:58:00,076 INFO  [PinpadMessageInterpreter] [Thread-3] GLOSA_CONFIRMAR_MONT : ***TARJETA ABCVISA***
2022-04-19 13:58:00,076 INFO  [PinpadMessageInterpreter] [Thread-3] FLAG_SOLICITUD_AUTEN : 03
2022-04-19 13:58:00,078 INFO  [SerialDriver] [Thread-3] Reconnecting Serialdriver: PPVX805TBK
2022-04-19 13:58:00,082 INFO  [CommPortIdentifier] [Thread-3] CommPortIdentifier:static initialization(), OS: Windows 10, arch: amd64
2022-04-19 13:58:00,082 INFO  [CommPortIdentifier] [Thread-3] Load the driver.
2022-04-19 13:58:00,086 INFO  [RXTXCommDriver] [Thread-3] RXTXCommDriver : static initializer.
2022-04-19 13:58:00,087 INFO  [SerialManager] [Thread-3] Load native library.
2022-04-19 13:58:00,088 INFO  [NativeResource] [Thread-3] Load lib: NRJavaSerial
2022-04-19 13:58:00,089 INFO  [NativeResource] [Thread-3] Loading from file: /native/windows/x86_64/libNRJavaSerial.dll
2022-04-19 13:58:00,093 INFO  [NativeResource] [Thread-3] Copy resources to: C:\Users\ancud\AppData\Local\Temp\libNRJavaSerial_ancud_0\libNRJavaSerial.dll
2022-04-19 13:58:00,114 INFO  [NativeResource] [Thread-3] Load resource from absolute path: C:\Users\ancud\AppData\Local\Temp\libNRJavaSerial_ancud_0\libNRJavaSerial.dll
2022-04-19 13:58:00,135 INFO  [CommPortIdentifier] [Thread-3] static CommPortIdentifier:getPortIdentifiers()
2022-04-19 13:58:00,135 INFO  [RXTXCommDriver] [Thread-3] RXTXCommDriver:initialize(), osName: Windows 10
2022-04-19 13:58:00,136 INFO  [RXTXCommDriver] [Thread-3] scanning device directory //./ for ports of type 1
2022-04-19 13:58:00,261 INFO  [RXTXCommDriver] [Thread-3] RXTXCommDriver:initialize(), osName: Windows 10
2022-04-19 13:58:00,262 INFO  [RXTXCommDriver] [Thread-3] scanning device directory //./ for ports of type 1
2022-04-19 13:58:00,391 INFO  [CommPortIdentifier] [Thread-3] Have not implemented native_psmisc_report_owner(PortName)); in CommPortIdentifier
2022-04-19 13:58:00,391 INFO  [RXTXCommDriver] [Thread-3] RXTXCommDriver:getCommPort(COM9,1)
2022-04-19 13:58:00,405 INFO  [RxTxSimpleSerialNativeLibWrapperImpl] [Thread-3] Connected to serial port [COM9] for LogicalDevice [PPVX805TBK]
2022-04-19 13:58:04,424 INFO  [TransbankVx805Intertpreter] [Thread-3] PINPAD Response Message
2022-04-19 13:58:04,425 INFO  [PinpadMessageInterpreter] [Thread-3] COMANDO              : 0810
2022-04-19 13:58:04,425 INFO  [PinpadMessageInterpreter] [Thread-3] CODIGO_RESPUESTA     : 99
2022-04-19 13:58:04,426 ERROR [TransbankVx805Intertpreter] [Thread-3] Can not parse message 0810
com.synthesis.vtolClientLib.exception.UnparseableDataException: 'buffer overrun' when trying to read field: INDICADOR_CONTEXTO
	at com.synthesis.vtolClientLib.pinpad.PinpadMessageInterpreter.readField(PinpadMessageInterpreter.java:104)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.TransbankVx805Intertpreter.parse0810(TransbankVx805Intertpreter.java:563)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.TransbankVx805Intertpreter.parseMessage(TransbankVx805Intertpreter.java:117)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.PinpadDriver.processEvent(PinpadDriver.java:181)
	at com.synthesis.vtolClientLib.deviceAdapters.AbstractDriver.run(AbstractDriver.java:139)
2022-04-19 13:58:04,428 INFO  [PinpadDriver] [Thread-3] Processing Pinpad Response
2022-04-19 13:58:04,428 INFO  [PinpadDriver] [Thread-3] Creating Message for Response 0810
2022-04-19 13:58:04,428 ERROR [PinpadDriver] [Thread-3] Response: 0810  Retorno: 99
2022-04-19 13:58:04,429 INFO  [AbstractDriver] [Thread-3] [LogicalName: PPVX805TBK DriverID: 1650387357579 Driver: class cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.PinpadDriver] Processed Event: Event[id=1650387356977,type=RTA_0810,device=pinPad,context=com.synthesis.vtolClientLib.VtolContextRepresentation@26bd5f19,error=<null>]
2022-04-19 13:58:04,429 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] Module: crdb
2022-04-19 13:58:04,429 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] Message Type: SaleOnUs
2022-04-19 13:58:04,430 INFO  [ValidateOnUsCrDbSaleMessageRequiredFieldsRule] [Thread-0] Executing: class cl.com.synthesis.vtol.clientTbk.business.rules.ValidateOnUsCrDbSaleMessageRequiredFieldsRule
2022-04-19 13:58:04,430 INFO  [ValidateOnUsCrDbSaleMessageRequiredFieldsRule] [Thread-0] Validating Sale OnUs data.
2022-04-19 13:58:04,431 ERROR [ValidateOnUsCrDbSaleMessageRequiredFieldsRule] [Thread-0] Error returned by the Pinpad: 99 - Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
2022-04-19 13:58:04,431 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] ResponseToPosException - ERROR_CONEXION: Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
2022-04-19 13:58:04,432 INFO  [LibToPosInterpreter] [ApacheWorkerThread-0] Response message: {1:092;2:90;1010:1650387478110;1027:099;1028:Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout}
2022-04-19 13:58:04,502 INFO  [TcpIpCommunication] [VtolLibService] Accepting socket from ip: 127.0.0.1 - port: 50464 - soTimeOut: 180000
2022-04-19 13:58:04,503 INFO  [PosToLibInterpreter] [ApacheWorkerThread-0] Request: {1008:CANCEL;2:90;1:092;11:closeSession}
2022-04-19 13:58:04,503 INFO  [IntegrationApi] [ApacheWorkerThread-0] Closing SESSION: RollbackSession
2022-04-19 13:58:04,504 INFO  [EventManager] [Thread-0] Closing session
2022-04-19 13:58:04,504 INFO  [JavaBC] [Thread-0] Close session
```

----
            
#KAS_Canete_254 - 192.2.254.244
Ultima Venta ABC: 2021 | Ultima Venta Webpay 29 Marzo

##Errores Detectados en Vtol Brigde
```
2022-04-19 10:47:24 ERROR Server:127 - 718:Cierre de lote requerido debido a cambio de moneda
java.lang.Exception: 718:Cierre de lote requerido debido a cambio de moneda
	at cl.acid.abcdin.transaction.VtolClient.checkResponseCode(VtolClient.java:299) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.authorization(VtolClient.java:195) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:608) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-04-19 10:47:24 INFO  Server:56 - onMessage : org.java_websocket.WebSocketImpl@13776ad0: {"type":"reject"}
2022-04-19 10:47:24 INFO  Server:101 - reject
2022-04-19 10:47:25 INFO  VtolClient:289 - ****** checkResponseCode :1110:0
1010:1650376036032
1028:Ok
1027:000
2:90
1:165
```
##Errores Detectados en Vtol Client

```
2022-03-17 18:11:45,873 INFO  [TransbankVx805Intertpreter] [Thread-3] PINPAD Request Message
2022-03-17 18:11:45,873 INFO  [PinpadMessageInterpreter] [Thread-3] COMANDO              : 0800
2022-03-17 18:11:45,874 INFO  [PinpadMessageInterpreter] [Thread-3] INDICADOR_CONTEXTO   : 0
2022-03-17 18:11:45,874 INFO  [PinpadMessageInterpreter] [Thread-3] LOCAL_COMERCIO_ON_US : 07
2022-03-17 18:11:45,874 INFO  [PinpadMessageInterpreter] [Thread-3] WORKING_KEY_TRACK    : 55769922FB6672E5BF7FEC05256A23F5
2022-03-17 18:11:45,874 INFO  [PinpadMessageInterpreter] [Thread-3] WORKING_KEY_PIN      : A04A98601D3BC45EF9BB0785127A6C67
2022-03-17 18:11:45,874 INFO  [PinpadMessageInterpreter] [Thread-3] MONTO                : 60998000
2022-03-17 18:11:45,874 INFO  [PinpadMessageInterpreter] [Thread-3] LISTA_MONTOS_VUELTOS : 100000;500000;1000000;2000000
2022-03-17 18:11:45,874 INFO  [PinpadMessageInterpreter] [Thread-3] MONTO_VUELTO         : 0
2022-03-17 18:11:45,875 INFO  [PinpadMessageInterpreter] [Thread-3] FLAG_CONFIRMAR_MONTO : Y
2022-03-17 18:11:45,875 INFO  [PinpadMessageInterpreter] [Thread-3] GLOSA_CONFIRMAR_MONT : 
2022-03-17 18:11:45,875 INFO  [PinpadMessageInterpreter] [Thread-3] GLOSA_CONFIRMAR_MONT : 1 cuotas 609980
2022-03-17 18:11:45,875 INFO  [PinpadMessageInterpreter] [Thread-3] GLOSA_CONFIRMAR_MONT : 
2022-03-17 18:11:45,875 INFO  [PinpadMessageInterpreter] [Thread-3] GLOSA_CONFIRMAR_MONT : ***TARJETA ABCVISA***
2022-03-17 18:11:45,875 INFO  [PinpadMessageInterpreter] [Thread-3] FLAG_SOLICITUD_AUTEN : 03
2022-03-17 18:11:45,877 INFO  [SerialDriver] [Thread-3] Reconnecting Serialdriver: PPVX805TBK
2022-03-17 18:11:45,883 INFO  [CommPortIdentifier] [Thread-3] CommPortIdentifier:static initialization(), OS: Windows 10, arch: amd64
2022-03-17 18:11:45,883 INFO  [CommPortIdentifier] [Thread-3] Load the driver.
2022-03-17 18:11:45,887 INFO  [RXTXCommDriver] [Thread-3] RXTXCommDriver : static initializer.
2022-03-17 18:11:45,888 INFO  [SerialManager] [Thread-3] Load native library.
2022-03-17 18:11:45,890 INFO  [NativeResource] [Thread-3] Load lib: NRJavaSerial
2022-03-17 18:11:45,891 INFO  [NativeResource] [Thread-3] Loading from file: /native/windows/x86_64/libNRJavaSerial.dll
2022-03-17 18:11:45,901 INFO  [NativeResource] [Thread-3] Copy resources to: C:\Users\totem\AppData\Local\Temp\libNRJavaSerial_totem_0\libNRJavaSerial.dll
2022-03-17 18:11:45,928 INFO  [NativeResource] [Thread-3] Load resource from absolute path: C:\Users\totem\AppData\Local\Temp\libNRJavaSerial_totem_0\libNRJavaSerial.dll
2022-03-17 18:11:45,937 INFO  [CommPortIdentifier] [Thread-3] static CommPortIdentifier:getPortIdentifiers()
2022-03-17 18:11:45,938 INFO  [RXTXCommDriver] [Thread-3] RXTXCommDriver:initialize(), osName: Windows 10
2022-03-17 18:11:45,939 INFO  [RXTXCommDriver] [Thread-3] scanning device directory //./ for ports of type 1
2022-03-17 18:11:46,079 INFO  [RXTXCommDriver] [Thread-3] RXTXCommDriver:initialize(), osName: Windows 10
2022-03-17 18:11:46,080 INFO  [RXTXCommDriver] [Thread-3] scanning device directory //./ for ports of type 1
2022-03-17 18:11:46,211 INFO  [CommPortIdentifier] [Thread-3] Have not implemented native_psmisc_report_owner(PortName)); in CommPortIdentifier
2022-03-17 18:11:46,211 INFO  [RXTXCommDriver] [Thread-3] RXTXCommDriver:getCommPort(COM9,1)
2022-03-17 18:11:46,223 INFO  [RxTxSimpleSerialNativeLibWrapperImpl] [Thread-3] Connected to serial port [COM9] for LogicalDevice [PPVX805TBK]
2022-03-17 18:12:18,386 INFO  [TransbankVx805Intertpreter] [Thread-3] PINPAD Response Message
2022-03-17 18:12:18,386 INFO  [PinpadMessageInterpreter] [Thread-3] COMANDO              : 0810
2022-03-17 18:12:18,387 INFO  [PinpadMessageInterpreter] [Thread-3] CODIGO_RESPUESTA     : 99
2022-03-17 18:12:18,391 ERROR [TransbankVx805Intertpreter] [Thread-3] Can not parse message 0810
com.synthesis.vtolClientLib.exception.UnparseableDataException: 'buffer overrun' when trying to read field: INDICADOR_CONTEXTO
	at com.synthesis.vtolClientLib.pinpad.PinpadMessageInterpreter.readField(PinpadMessageInterpreter.java:104)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.TransbankVx805Intertpreter.parse0810(TransbankVx805Intertpreter.java:563)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.TransbankVx805Intertpreter.parseMessage(TransbankVx805Intertpreter.java:117)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.PinpadDriver.processEvent(PinpadDriver.java:181)
	at com.synthesis.vtolClientLib.deviceAdapters.AbstractDriver.run(AbstractDriver.java:139)
2022-03-17 18:12:18,396 INFO  [PinpadDriver] [Thread-3] Processing Pinpad Response
2022-03-17 18:12:18,396 INFO  [PinpadDriver] [Thread-3] Creating Message for Response 0810
2022-03-17 18:12:18,397 ERROR [PinpadDriver] [Thread-3] Response: 0810  Retorno: 99
2022-03-17 18:12:18,398 INFO  [AbstractDriver] [Thread-3] [LogicalName: PPVX805TBK DriverID: 1647551413048 Driver: class cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.PinpadDriver] Processed Event: Event[id=1647551412503,type=RTA_0810,device=pinPad,context=com.synthesis.vtolClientLib.VtolContextRepresentation@39155aed,error=<null>]
2022-03-17 18:12:18,400 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] Module: crdb
2022-03-17 18:12:18,401 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] Message Type: SaleOnUs
2022-03-17 18:12:18,405 INFO  [ValidateOnUsCrDbSaleMessageRequiredFieldsRule] [Thread-0] Executing: class cl.com.synthesis.vtol.clientTbk.business.rules.ValidateOnUsCrDbSaleMessageRequiredFieldsRule
2022-03-17 18:12:18,405 INFO  [ValidateOnUsCrDbSaleMessageRequiredFieldsRule] [Thread-0] Validating Sale OnUs data.
2022-03-17 18:12:18,405 ERROR [ValidateOnUsCrDbSaleMessageRequiredFieldsRule] [Thread-0] Error returned by the Pinpad: 99 - Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
2022-03-17 18:12:18,407 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] ResponseToPosException - ERROR_CONEXION: Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
2022-03-17 18:12:18,410 INFO  [LibToPosInterpreter] [ApacheWorkerThread-0] Response message: {1:254;2:90;1010:1647551504803;1027:099;1028:Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout}
2022-03-17 18:12:18,491 INFO  [TcpIpCommunication] [VtolLibService] Accepting socket from ip: 127.0.0.1 - port: 57504 - soTimeOut: 180000
2022-03-17 18:12:18,492 INFO  [PosToLibInterpreter] [ApacheWorkerThread-0] Request: {1008:CANCEL;2:90;1:254;11:closeSession}
2022-03-17 18:12:18,494 INFO  [IntegrationApi] [ApacheWorkerThread-0] Closing SESSION: RollbackSession
2022-03-17 18:12:18,494 INFO  [EventManager] [Thread-0] Closing session
2022-03-17 18:12:18,494 INFO  [JavaBC] [Thread-0] Close session
```

----

#KAS_Iquique_016 - 192.2.16.244
No vende con ningún método de pago 

##Errores Detectados en Vtol Bridge
No encripta Data:
```
2022-04-06 18:50:54 INFO  VtolClient:252 - getConfiguration 1110:0
1010:1649281854579
1028:Ok
1027:000
113:{encab1=ABCDIN Intermodal La Cisterna, encab2=ABCDIN Intermodal La Cisterna, terminalDolar=H3PCF36246359208, propina=N, encab3=Santiago, encab4=Cod Comercio - Version APP, baudiosPinPad=9600, pie1=Gracias por su Compra, pie2=Original Comercio - Copia Cliente, pie3=Acepto Pagar según contrato con Emisor, empleado=N, moneda=CL, maxCuotasN=12, anulacion=Y, pan=N, pie4=Acepto el cargo en mi tarjeta pagado�?, panManual=N, cashBack=N, pie5=en el numero y monto de cuotas�?, pie6=las que ya incluyen intereses, pie7=operación sujeta a impuesto�?, debito=N, tipoDeCaja=Caja Host, venta=Y, monMinPesosChilenos=500, timeOut4Digitos=0, montoVuelto1=1000, montoVuelto3=10000, monMinDolares=100, montoVuelto2=5000, terminal=H3PCF36246359208, version=821, montoVuelto4=20000, timeOut=60, comercioDolar=597036246359, comercio=597036246359, boleta=N}
2:90
1:016

2022-04-06 18:50:54 INFO  VtolClient:289 - ****** checkResponseCode :1110:0
1010:1649281854579
1028:Ok
1027:000
113:{encab1=ABCDIN Intermodal La Cisterna, encab2=ABCDIN Intermodal La Cisterna, terminalDolar=H3PCF36246359208, propina=N, encab3=Santiago, encab4=Cod Comercio - Version APP, baudiosPinPad=9600, pie1=Gracias por su Compra, pie2=Original Comercio - Copia Cliente, pie3=Acepto Pagar según contrato con Emisor, empleado=N, moneda=CL, maxCuotasN=12, anulacion=Y, pan=N, pie4=Acepto el cargo en mi tarjeta pagado�?, panManual=N, cashBack=N, pie5=en el numero y monto de cuotas�?, pie6=las que ya incluyen intereses, pie7=operación sujeta a impuesto�?, debito=N, tipoDeCaja=Caja Host, venta=Y, monMinPesosChilenos=500, timeOut4Digitos=0, montoVuelto1=1000, montoVuelto3=10000, monMinDolares=100, montoVuelto2=5000, terminal=H3PCF36246359208, version=821, montoVuelto4=20000, timeOut=60, comercioDolar=597036246359, comercio=597036246359, boleta=N}
2:90
1:016

2022-04-06 18:50:55 INFO  CSI:189 - Plain Request GETKEKAUT: <?xml version='1.0' encoding='ISO-8859-1'?><request_auth>
<service_id>GETKEKAUT</service_id>
<subtype_service>00CSK1001601</subtype_service>
<pan>2022040618505510016</pan>
<ctype>CC</ctype>
<ctext>WKPINAUT10016</ctext>
<interface_id>CMDCSI</interface_id>
<customer_id>K1001601</customer_id>
<client_ip>192.2.16.101</client_ip>
</request_auth>

2022-04-06 18:50:55 INFO  CSI:203 - Encrypted Request GETKEKAUT: <?xml version='1.0' encoding='ISO-8859-1'?><request_auth>
<service_id>GETKEKAUT</service_id>
<subtype_service>00CSK1001601</subtype_service>
<pan>null</pan>
<ctype>null</ctype>
<ctext>null</ctext>
<interface_id>null</interface_id>
<customer_id>null</customer_id>
<client_ip>null</client_ip>
</request_auth>

2022-04-06 18:50:55 ERROR VtolClient:519 - null
java.lang.NullPointerException: null
	at cl.stx.lib.mac.LibMacStx.hexStringToByteArray(LibMacStx.java:167) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.stx.lib.mac.LibMacStx.g81ae7641a172b3763c8918efe1(LibMacStx.java:161) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.stx.lib.mac.LibMacStx.gb356d46e0118509a354(LibMacStx.java:45) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.stx.lib.mac.LibMacStx.genMacCsi(LibMacStx.java:29) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.CSI.signature(CSI.java:82) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.CSI.sendCommand(CSI.java:205) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.CSI.getKEKAUT(CSI.java:88) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:516) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-04-06 18:50:55 ERROR VtolClient:616 - Caught event
java.lang.Exception: El sistema se encuentra fuera de servicio
	at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:520) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-04-06 18:50:55 INFO  VtolClient:289 - ****** checkResponseCode :1110:0
1010:1649281854579
1028:Ok
1027:000
2:90
1:016
```
----

#KAS_La_Serena_165 - 192.2.165.101
No vende con ningún método de pago

##Errores Detectados en Vtol Brigde:

```
2022-04-19 10:47:16 INFO  VtolClient:221 - leerTarjeta : ****reading Tue Apr 19 10:47:16 CLST 2022
2022-04-19 10:47:22 INFO  VtolClient:223 - leerTarjeta : ****reading ended Tue Apr 19 10:47:22 CLST 2022
2022-04-19 10:47:22 INFO  VtolClient:289 - ****** checkResponseCode :1103:2022041911141720
1102:MT
1010:1650376036032
1028:Ok
1027:000
8:621996
1110:0
2:90
25:20220419104716
1:165

2022-04-19 10:47:24 INFO  VtolClient:289 - ****** checkResponseCode :1010:1650376036032
1028:Cierre de lote requerido debido a cambio de moneda
1027:718
25:20220419104722
2:90
1:165

2022-04-19 10:47:24 ERROR VtolClient:616 - Caught event
java.lang.Exception: 718:Cierre de lote requerido debido a cambio de moneda
	at cl.acid.abcdin.transaction.VtolClient.checkResponseCode(VtolClient.java:299) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.authorization(VtolClient.java:195) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:608) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-04-19 10:47:24 INFO  VtolClient:289 - ****** checkResponseCode :1110:0
1010:1650376036032
1028:Ok
1027:000
2:90
1:165

----

2022-04-19 13:31:00 INFO  VtolClient:339 - closeSession :1110:0
1010:1650385826356
1028:Ok
1027:000
2:90
1:165

2022-04-19 13:31:00 ERROR Server:127 - El sistema se encuentra fuera de servicio para SOLKEYTRK o RECTRACK2
java.lang.Exception: El sistema se encuentra fuera de servicio para SOLKEYTRK o RECTRACK2
	at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:533) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-04-19 13:31:00 INFO  Server:56 - onMessage : org.java_websocket.WebSocketImpl@34a30f6f: {"type":"reject"}
2022-04-19 13:31:00 INFO  Server:101 - reject
2022-04-19 13:31:01 INFO  VtolClient:289 - ****** checkResponseCode :1110:0
1010:1650385826356
1028:Ok
1027:000
2:90

```

##Errores Detectados en Vtol Client


```
2022-04-19 13:30:28,028 INFO  [TransbankVx805Intertpreter] [Thread-3] PINPAD Request Message
2022-04-19 13:30:28,028 INFO  [PinpadMessageInterpreter] [Thread-3] COMANDO              : 0800
2022-04-19 13:30:28,028 INFO  [PinpadMessageInterpreter] [Thread-3] INDICADOR_CONTEXTO   : 0
2022-04-19 13:30:28,028 INFO  [PinpadMessageInterpreter] [Thread-3] LOCAL_COMERCIO_ON_US : 07
2022-04-19 13:30:28,028 INFO  [PinpadMessageInterpreter] [Thread-3] WORKING_KEY_TRACK    : 55769922FB6672E5BF7FEC05256A23F5
2022-04-19 13:30:28,028 INFO  [PinpadMessageInterpreter] [Thread-3] WORKING_KEY_PIN      : A04A98601D3BC45EF9BB0785127A6C67
2022-04-19 13:30:28,028 INFO  [PinpadMessageInterpreter] [Thread-3] MONTO                : 20898000
2022-04-19 13:30:28,028 INFO  [PinpadMessageInterpreter] [Thread-3] LISTA_MONTOS_VUELTOS : 100000;500000;1000000;2000000
2022-04-19 13:30:28,028 INFO  [PinpadMessageInterpreter] [Thread-3] MONTO_VUELTO         : 0
2022-04-19 13:30:28,028 INFO  [PinpadMessageInterpreter] [Thread-3] FLAG_CONFIRMAR_MONTO : Y
2022-04-19 13:30:28,028 INFO  [PinpadMessageInterpreter] [Thread-3] GLOSA_CONFIRMAR_MONT : 
2022-04-19 13:30:28,029 INFO  [PinpadMessageInterpreter] [Thread-3] GLOSA_CONFIRMAR_MONT : 12 cuotas 21188
2022-04-19 13:30:28,029 INFO  [PinpadMessageInterpreter] [Thread-3] GLOSA_CONFIRMAR_MONT : 
2022-04-19 13:30:28,029 INFO  [PinpadMessageInterpreter] [Thread-3] GLOSA_CONFIRMAR_MONT : ***TARJETA ABCVISA***
2022-04-19 13:30:28,029 INFO  [PinpadMessageInterpreter] [Thread-3] FLAG_SOLICITUD_AUTEN : 03
2022-04-19 13:31:00,311 INFO  [TransbankVx805Intertpreter] [Thread-3] PINPAD Response Message
2022-04-19 13:31:00,312 INFO  [PinpadMessageInterpreter] [Thread-3] COMANDO              : 0810
2022-04-19 13:31:00,312 INFO  [PinpadMessageInterpreter] [Thread-3] CODIGO_RESPUESTA     : 99
2022-04-19 13:31:00,312 ERROR [TransbankVx805Intertpreter] [Thread-3] Can not parse message 0810
com.synthesis.vtolClientLib.exception.UnparseableDataException: 'buffer overrun' when trying to read field: INDICADOR_CONTEXTO
	at com.synthesis.vtolClientLib.pinpad.PinpadMessageInterpreter.readField(PinpadMessageInterpreter.java:104)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.TransbankVx805Intertpreter.parse0810(TransbankVx805Intertpreter.java:563)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.TransbankVx805Intertpreter.parseMessage(TransbankVx805Intertpreter.java:117)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.PinpadDriver.processEvent(PinpadDriver.java:181)
	at com.synthesis.vtolClientLib.deviceAdapters.AbstractDriver.run(AbstractDriver.java:139)
2022-04-19 13:31:00,313 INFO  [PinpadDriver] [Thread-3] Processing Pinpad Response
2022-04-19 13:31:00,314 INFO  [PinpadDriver] [Thread-3] Creating Message for Response 0810
2022-04-19 13:31:00,314 ERROR [PinpadDriver] [Thread-3] Response: 0810  Retorno: 99
2022-04-19 13:31:00,314 INFO  [AbstractDriver] [Thread-3] [LogicalName: PPVX805TBK DriverID: 1649807030490 Driver: class cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.PinpadDriver] Processed Event: Event[id=1649807029903,type=RTA_0810,device=pinPad,context=com.synthesis.vtolClientLib.VtolContextRepresentation@7f421786,error=<null>]
2022-04-19 13:31:00,315 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] Module: crdb
2022-04-19 13:31:00,316 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] Message Type: SaleOnUs
2022-04-19 13:31:00,318 INFO  [ValidateOnUsCrDbSaleMessageRequiredFieldsRule] [Thread-0] Executing: class cl.com.synthesis.vtol.clientTbk.business.rules.ValidateOnUsCrDbSaleMessageRequiredFieldsRule
2022-04-19 13:31:00,318 INFO  [ValidateOnUsCrDbSaleMessageRequiredFieldsRule] [Thread-0] Validating Sale OnUs data.
2022-04-19 13:31:00,319 ERROR [ValidateOnUsCrDbSaleMessageRequiredFieldsRule] [Thread-0] Error returned by the Pinpad: 99 - Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
2022-04-19 13:31:00,319 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] ResponseToPosException - ERROR_CONEXION: Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
2022-04-19 13:31:00,322 INFO  [LibToPosInterpreter] [ApacheWorkerThread-0] Response message: {1:165;2:90;1010:1650385826356;1027:099;1028:Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout}
2022-04-19 13:31:00,363 INFO  [TcpIpCommunication] [VtolLibService] Accepting socket from ip: 127.0.0.1 - port: 56341 - soTimeOut: 180000
2022-04-19 13:31:00,365 INFO  [PosToLibInterpreter] [ApacheWorkerThread-0] Request: {1008:CANCEL;2:90;1:165;11:closeSession}
2022-04-19 13:31:00,365 INFO  [IntegrationApi] [ApacheWorkerThread-0] Closing SESSION: RollbackSession
2022-04-19 13:31:00,366 INFO  [EventManager] [Thread-0] Closing session
2022-04-19 13:31:00,366 INFO  [JavaBC] [Thread-0] Close session
```

----

KAS_Osorno_281 - 192.2.81.101
Ultima Venta ABC: 14 Abril | Ultima Venta Webpay 07 Febrero

##Errores Detectados en Vtol Bridge


```
2022-04-14 17:47:38 ERROR VtolClient:532 - 099:Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
java.lang.Exception: 099:Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
	at cl.acid.abcdin.transaction.VtolClient.checkResponseCode(VtolClient.java:299) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.saleOnUs(VtolClient.java:163) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:527) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-04-14 17:47:38 ERROR VtolClient:616 - Caught event
java.lang.Exception: El sistema se encuentra fuera de servicio para SOLKEYTRK o RECTRACK2
	at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:533) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-04-14 17:47:38 INFO  VtolClient:289 - ****** checkResponseCode :1110:0
1010:1649969225642
1028:Ok
1027:000
2:90
1:281

2022-04-14 17:45:40 ERROR VtolClient:532 - 099:Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
java.lang.Exception: 099:Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
	at cl.acid.abcdin.transaction.VtolClient.checkResponseCode(VtolClient.java:299) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.saleOnUs(VtolClient.java:163) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:527) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-04-14 17:45:40 ERROR VtolClient:616 - Caught event
java.lang.Exception: El sistema se encuentra fuera de servicio para SOLKEYTRK o RECTRACK2
	at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:533) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-04-14 17:45:40 INFO  VtolClient:289 - ****** checkResponseCode :1110:0
1010:1649969090939
1028:Ok
1027:000
2:90
1:281

```

##Errores Detectados en Vtol Client


```
2022-04-16 13:37:52,090 INFO  [PinpadMessageInterpreter] [Thread-3] COMANDO              : 0100
2022-04-16 13:37:52,090 INFO  [PinpadMessageInterpreter] [Thread-3] LOCAL_COMERCIO_ON_US : 00
2022-04-16 13:37:52,090 INFO  [PinpadMessageInterpreter] [Thread-3] FLAG_ENTREGA_BIN     : Y
2022-04-16 13:37:52,091 INFO  [PinpadMessageInterpreter] [Thread-3] FLAG_TRX_OFF_LINE    : N
2022-04-16 13:37:52,091 INFO  [PinpadMessageInterpreter] [Thread-3] FLAG_AUTOSERVICIO    : N
2022-04-16 13:37:52,091 INFO  [PinpadMessageInterpreter] [Thread-3] MONTO                : 21898000
2022-04-16 13:37:52,091 INFO  [PinpadMessageInterpreter] [Thread-3] CODIGO_MONEDA        : CL
2022-04-16 13:37:52,091 INFO  [PinpadMessageInterpreter] [Thread-3] TIPO_TARJETA         : CR
2022-04-16 13:37:52,091 INFO  [PinpadMessageInterpreter] [Thread-3] LISTA_MONTOS_VUELTOS : 100000;500000;1000000;2000000
2022-04-16 13:37:52,091 INFO  [PinpadMessageInterpreter] [Thread-3] MONTO_VUELTO         : 0
2022-04-16 13:37:52,091 INFO  [PinpadMessageInterpreter] [Thread-3] MONTO_PROPINA_DONACI : 0
2022-04-16 13:37:55,034 INFO  [TransbankVx805Intertpreter] [Thread-3] PINPAD Response Message
2022-04-16 13:37:55,035 INFO  [PinpadMessageInterpreter] [Thread-3] COMANDO              : 0110
2022-04-16 13:37:55,035 INFO  [PinpadMessageInterpreter] [Thread-3] CODIGO_RESPUESTA     : 99
2022-04-16 13:37:55,035 ERROR [TransbankVx805Intertpreter] [Thread-3] Can not parse message 0110
com.synthesis.vtolClientLib.exception.UnparseableDataException: 'buffer overrun' when trying to read field: INDICADOR_CONTEXTO
	at com.synthesis.vtolClientLib.pinpad.PinpadMessageInterpreter.readField(PinpadMessageInterpreter.java:104)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.TransbankVx805Intertpreter.parse0110(TransbankVx805Intertpreter.java:327)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.TransbankVx805Intertpreter.parseMessage(TransbankVx805Intertpreter.java:99)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.PinpadDriver.processEvent(PinpadDriver.java:181)
	at com.synthesis.vtolClientLib.deviceAdapters.AbstractDriver.run(AbstractDriver.java:139)
2022-04-16 13:37:55,036 INFO  [PinpadDriver] [Thread-3] Processing Pinpad Response
2022-04-16 13:37:55,036 INFO  [PinpadDriver] [Thread-3] Creating Message for Response 0110
2022-04-16 13:37:55,036 ERROR [PinpadDriver] [Thread-3] Response: 0110  Retorno: 99
2022-04-16 13:37:55,036 INFO  [AbstractDriver] [Thread-3] [LogicalName: PPVX805TBK DriverID: 1649901293825 Driver: class cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.PinpadDriver] Processed Event: Event[id=1649901293363,type=DATOS_TARJETA,device=pinPad,context=com.synthesis.vtolClientLib.VtolContextRepresentation@3ea42506,error=<null>]
2022-04-16 13:37:55,037 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] Module: crdb
2022-04-16 13:37:55,037 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] Message Type: Sale
2022-04-16 13:37:55,039 INFO  [ValidateVtolCrDbSaleMessageReadCardRule] [Thread-0] Executing: class cl.com.synthesis.vtol.clientTbk.business.rules.ValidateVtolCrDbSaleMessageReadCardRule
2022-04-16 13:37:55,039 INFO  [ValidateVtolCrDbSaleMessageReadCardRule] [Thread-0] Validating Read Card data
2022-04-16 13:37:55,040 ERROR [ValidateVtolCrDbSaleMessageReadCardRule] [Thread-0] Error returned by the Pinpad: 99 - Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
2022-04-16 13:37:55,040 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] ResponseToPosException - ERROR_CONEXION: Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
2022-04-16 13:37:55,043 INFO  [LibToPosInterpreter] [ApacheWorkerThread-0] Response message: {1:281;2:90;1010:1649969564701;1027:099;1028:Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout;25:20220416133750}
2022-04-16 13:37:55,089 INFO  [TcpIpCommunication] [VtolLibService] Accepting socket from ip: 127.0.0.1 - port: 59375 - soTimeOut: 180000
2022-04-16 13:37:55,090 INFO  [PosToLibInterpreter] [ApacheWorkerThread-0] Request: {1008:CANCEL;2:90;1:281;11:closeSession}
2022-04-16 13:37:55,090 INFO  [IntegrationApi] [ApacheWorkerThread-0] Closing SESSION: RollbackSession
2022-04-16 13:37:55,090 INFO  [EventManager] [Thread-0] Closing session
2022-04-16 13:37:55,090 INFO  [JavaBC] [Thread-0] Close session
```

----

#KAS_Punta_Arenas_096 - 192.2.96.244
Ultima Venta ABC: Febrero 2021 | Ultima Venta Webpay: 21 Marzo

##Errores Detectados en Vtol Bridge:


```
2022-03-19 16:46:36 ERROR Server:127 - 999:La sesion debe estar creada antes de enviar un requerimiento.
java.lang.Exception: 999:La sesion debe estar creada antes de enviar un requerimiento.
	at cl.acid.abcdin.transaction.VtolClient.checkResponseCode(VtolClient.java:299) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.getOriginalSale(VtolClient.java:381) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:96) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-03-19 16:46:36 INFO  Server:44 - This is info : 0:0:0:0:0:0:0:1 connected!
2022-03-19 16:46:36 INFO  Server:149 - websocket onError
2022-03-19 16:46:44 ERROR Server:127 - Timeout waiting server response.
ar.com.synthesis.vtol.client.TimeoutClientException: Timeout waiting server response.
	at ar.com.synthesis.vtol.client.VtolConnectionManager.send(VtolConnectionManager.java:179) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at ar.com.synthesis.vtol.client.VtolConnectionManager.send(VtolConnectionManager.java:79) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at ar.com.synthesis.vtol.client.VtolNode.sendTransactionToVtol(VtolNode.java:291) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at ar.com.synthesis.vtol.client.VtolNode.sendTransaction(VtolNode.java:263) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.closeSession(VtolClient.java:333) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.closeCancelSession(VtolClient.java:318) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:103) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-03-19 16:46:44 INFO  Server:149 - websocket onError
2022-03-19 16:48:03 INFO  Server:44 - This is info : 0:0:0:0:0:0:0:1 connected!
2022-03-19 16:48:03 INFO  Server:56 - onMessage : org.java_websocket.WebSocketImpl@6229e7b4: {"type":"status"}
2022-03-19 16:48:03 INFO  Server:124 - done
2022-03-19 16:48:04 INFO  Server:44 - This is info : 0:0:0:0:0:0:0:1 connected!
2022-03-19 16:48:04 INFO  Server:56 - onMessage : org.java_websocket.WebSocketImpl@6e098d5c: {"type":"transaction","trxId":"138", "terminalId":20 ,
          "interestRate": "null" ,"amount":"12998000","cardType": "DB","ticket": "105138364","rut": "0", 
          "payments": "0", "paymentsAmount": "0", "totalCreditAmount": "000"}
2022-03-19 16:48:04 INFO  Server:64 - transaction
2022-03-19 16:48:05 INFO  VtolClient:266 - createSession 1010:1647719285317
1028:Ok
1027:000
2:90
1:096

----

2022-03-21 18:39:18 ERROR VtolClient:616 - Caught event
java.lang.Exception: 099:Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
	at cl.acid.abcdin.transaction.VtolClient.checkResponseCode(VtolClient.java:299) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.authorization(VtolClient.java:195) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:608) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-03-21 18:39:18 INFO  VtolClient:289 - ****** checkResponseCode :1028:La libreria esta procesando un reverso.
1027:104

2022-03-21 18:39:18 ERROR Server:127 - 099:Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
java.lang.Exception: 099:Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
	at cl.acid.abcdin.transaction.VtolClient.checkResponseCode(VtolClient.java:299) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.authorization(VtolClient.java:195) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:608) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-03-21 18:39:18 INFO  Server:56 - onMessage : org.java_websocket.WebSocketImpl@3f5b1b95: {"type":"reject"}
2022-03-21 18:39:18 INFO  Server:101 - reject
2022-03-21 18:39:18 INFO  VtolClient:289 - ****** checkResponseCode :1028:La libreria esta procesando un reverso.
1027:104

2022-03-21 18:39:18 ERROR Server:127 - 104:La libreria esta procesando un reverso.
java.lang.Exception: 104:La libreria esta procesando un reverso.
	at cl.acid.abcdin.transaction.VtolClient.checkResponseCode(VtolClient.java:299) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.closeSession(VtolClient.java:337) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.closeCancelSession(VtolClient.java:318) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:103) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-03-21 18:39:28 INFO  Server:44 - This is info : 0:0:0:0:0:0:0:1 connected!
2022-03-21 18:39:28 INFO  Server:56 - onMessage : org.java_websocket.WebSocketImpl@7f6ad5c9: {"type":"status"}
2022-03-21 18:39:28 INFO  Server:124 - done
2022-03-21 18:39:28 INFO  Server:44 - This is info : 0:0:0:0:0:0:0:1 connected!
2022-03-21 18:39:29 INFO  Server:56 - onMessage : org.java_websocket.WebSocketImpl@62de914e: {"type":"transaction","trxId":"139", "terminalId":20 ,
          "interestRate": "null" ,"amount":"61546000","cardType": "CR","ticket": "105138403","rut": "0", 
          "payments": "0", "paymentsAmount": "0", "totalCreditAmount": "000"}
2022-03-21 18:39:29 INFO  Server:64 - transaction
2022-03-21 18:39:29 INFO  VtolClient:266 - createSession 1028:La sesion ya se encuentra creada.
1027:101

----

2022-04-16 19:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-16 19:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-16 19:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-17 01:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-17 01:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-17 01:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-17 07:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-17 07:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-17 07:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-17 13:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-17 13:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-17 13:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-17 19:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-17 19:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-17 19:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-18 01:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-18 01:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-18 01:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-18 07:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-18 07:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-18 07:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-18 13:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-18 13:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-18 13:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-18 19:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-18 19:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-18 19:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-19 01:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-19 01:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-19 01:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-19 07:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-19 07:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-19 07:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-19 13:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-19 13:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-19 13:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-19 19:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-19 19:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-19 19:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-20 01:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-20 01:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-20 01:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-20 07:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-20 07:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-20 07:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA
2022-04-20 13:21:23 INFO  VtolClient:60 - properties loaded : {csiLocalIp=192.2.96.101, node=90, server=https://app.abcdin.cl/api/, csiInterfaceId=XMLCSI, csiSucursal=10096, codCanal=POS, csiId=K1009601, empresaId=1, csiServer=http://192.168.50.225:80/CSI_TrustedSelfServiceWeb/CSIv1001, tiendaId=096, csiNombreLlave=CSK1009601, store=096, sentryDSN=https://808901e08bd4451e8332a383e719f2ee@sentry.io/1290100, csiMacha=502AD1014AA1ADECC0CE31ECC25B0D864C2964CB1C0706F0}
2022-04-20 13:21:23 INFO  App:33 - **************AUTO Iniciando CIERRE CAJAAA
2022-04-20 13:21:23 INFO  App:37 - **************AUTO Fin CIERRE CAJA

```

##Errores Detectados en Vtol Client


```
2022-01-06 08:29:39,329 INFO  [SendConfirmationMessageProcess] [Thread-2] Construyendo el mensaje para SaveClosing
2022-01-06 08:29:39,343 INFO  [SendConfirmationMessageProcess] [Thread-2] Envio a VTOL: {114:0000;11:SaveClosing;30:597030776119;29:H3PCG30776119950;117:000000000000000000;2:90;25:20220106082939;71:False;116:0000;1:096;115:000000000000000000}
2022-01-06 08:29:39,498 INFO  [LibToPosInterpreter] [ApacheWorkerThread-0] Response message: {1:096;2:90;1010:1641468574112;1027:000;1028:Ok}
2022-01-06 08:29:49,418 ERROR [SendConfirmationMessageProcess] [Thread-2] Error enviando un msj de autorizacion a Vtol.
ar.com.synthesis.vtol.client.TimeoutClientException: Timeout waiting server response.
	at ar.com.synthesis.vtol.client.VtolConnectionManager.send(VtolConnectionManager.java:179)
	at ar.com.synthesis.vtol.client.VtolConnectionManager.send(VtolConnectionManager.java:79)
	at ar.com.synthesis.vtol.client.VtolNode.sendTransactionToVtol(VtolNode.java:291)
	at ar.com.synthesis.vtol.client.VtolNode.sendTransaction(VtolNode.java:263)
	at cl.com.synthesis.vtol.clientTbk.business.SendConfirmationMessageProcess.sendMessage(SendConfirmationMessageProcess.java:145)
	at cl.com.synthesis.vtol.clientTbk.business.SendConfirmationMessageProcess.run(SendConfirmationMessageProcess.java:79)
2022-01-06 08:29:54,434 INFO  [SendConfirmationMessageProcess] [Thread-2] Construyendo el mensaje para SaveClosing
2022-01-06 08:29:54,435 INFO  [SendConfirmationMessageProcess] [Thread-2] Envio a VTOL: {114:0000;11:SaveClosing;30:597030776119;29:H3PCG30776119950;117:000000000000000000;2:90;25:20220106082939;71:False;116:0000;1:096;115:000000000000000000}
2022-01-06 08:30:01,379 INFO  [SendConfirmationMessageProcess] [Thread-2] Respuesta de VTOL: {28:Aprobada;27:00;26:ISO8583;25:20220106083424;2:90;1:096}
2022-01-06 14:29:32,399 INFO  [TcpIpCommunication] [VtolLibService] Accepting socket from ip: 127.0.0.1 - port: 57560 - soTimeOut: 180000
2022-01-06 14:29:32,400 INFO  [PosToLibInterpreter] [ApacheWorkerThread-0] Request: {1008:CANCEL;2:90;1:096;11:closeSession}
2022-01-06 14:29:32,400 INFO  [IntegrationApi] [ApacheWorkerThread-0] Closing SESSION: RollbackSession
2022-01-06 14:29:32,401 INFO  [EventManager] [Thread-0] Closing session
```

#KAS_Rancagua_075 - 192.2.75.244
Ultima Venta ABC: Septiembre 2021 | Ultima Venta Webpay: 16 Abril

##Errores Detectados en Vtol Bridge

```
2022-04-20 16:32:34 INFO  VtolClient:339 - closeSession :1110:0
1010:1650483133841
1028:Ok
1027:000
2:90
1:075

2022-04-20 16:32:34 ERROR Server:127 - 718:Cierre de lote requerido debido a cambio de moneda
java.lang.Exception: 718:Cierre de lote requerido debido a cambio de moneda
	at cl.acid.abcdin.transaction.VtolClient.checkResponseCode(VtolClient.java:299) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.authorization(VtolClient.java:195) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:608) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
	at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
2022-04-20 16:32:35 INFO  Server:56 - onMessage : org.java_websocket.WebSocketImpl@182562f: {"type":"reject"}
2022-04-20 16:32:35 INFO  Server:101 - reject
2022-04-20 16:32:35 INFO  VtolClient:289 - ****** checkResponseCode :1110:0
1010:1650483133841
1028:Ok
1027:000
2:90
1:075
```

##Errores Detectados en Vtol Client

```
2022-04-19 12:51:56,725 INFO  [PinpadDriver] [Thread-3] Creating Command 0100
2022-04-19 12:51:56,726 INFO  [TransbankVx805Intertpreter] [Thread-3] PINPAD Request Message
2022-04-19 12:51:56,726 INFO  [PinpadMessageInterpreter] [Thread-3] COMANDO              : 0100
2022-04-19 12:51:56,726 INFO  [PinpadMessageInterpreter] [Thread-3] LOCAL_COMERCIO_ON_US : 00
2022-04-19 12:51:56,726 INFO  [PinpadMessageInterpreter] [Thread-3] FLAG_ENTREGA_BIN     : Y
2022-04-19 12:51:56,726 INFO  [PinpadMessageInterpreter] [Thread-3] FLAG_TRX_OFF_LINE    : N
2022-04-19 12:51:56,726 INFO  [PinpadMessageInterpreter] [Thread-3] FLAG_AUTOSERVICIO    : N
2022-04-19 12:51:56,727 INFO  [PinpadMessageInterpreter] [Thread-3] MONTO                : 38398000
2022-04-19 12:51:56,727 INFO  [PinpadMessageInterpreter] [Thread-3] CODIGO_MONEDA        : CL
2022-04-19 12:51:56,727 INFO  [PinpadMessageInterpreter] [Thread-3] TIPO_TARJETA         : DB
2022-04-19 12:51:56,727 INFO  [PinpadMessageInterpreter] [Thread-3] LISTA_MONTOS_VUELTOS : 100000;500000;1000000;2000000
2022-04-19 12:51:56,727 INFO  [PinpadMessageInterpreter] [Thread-3] MONTO_VUELTO         : 0
2022-04-19 12:51:56,728 INFO  [PinpadMessageInterpreter] [Thread-3] MONTO_PROPINA_DONACI : 0
2022-04-19 12:52:04,446 INFO  [TransbankVx805Intertpreter] [Thread-3] PINPAD Response Message
2022-04-19 12:52:04,446 INFO  [PinpadMessageInterpreter] [Thread-3] COMANDO              : 0110
2022-04-19 12:52:04,447 INFO  [PinpadMessageInterpreter] [Thread-3] CODIGO_RESPUESTA     : 99
2022-04-19 12:52:04,447 ERROR [TransbankVx805Intertpreter] [Thread-3] Can not parse message 0110
com.synthesis.vtolClientLib.exception.UnparseableDataException: 'buffer overrun' when trying to read field: INDICADOR_CONTEXTO
	at com.synthesis.vtolClientLib.pinpad.PinpadMessageInterpreter.readField(PinpadMessageInterpreter.java:104)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.TransbankVx805Intertpreter.parse0110(TransbankVx805Intertpreter.java:327)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.TransbankVx805Intertpreter.parseMessage(TransbankVx805Intertpreter.java:99)
	at cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.PinpadDriver.processEvent(PinpadDriver.java:181)
	at com.synthesis.vtolClientLib.deviceAdapters.AbstractDriver.run(AbstractDriver.java:139)
2022-04-19 12:52:04,448 INFO  [PinpadDriver] [Thread-3] Processing Pinpad Response
2022-04-19 12:52:04,448 INFO  [PinpadDriver] [Thread-3] Creating Message for Response 0110
2022-04-19 12:52:04,448 ERROR [PinpadDriver] [Thread-3] Response: 0110  Retorno: 99
2022-04-19 12:52:04,449 INFO  [AbstractDriver] [Thread-3] [LogicalName: PPVX805TBK DriverID: 1650382863477 Driver: class cl.com.synthesis.vtol.clientTbk.deviceAdapters.pinpad.PinpadDriver] Processed Event: Event[id=1650382862635,type=DATOS_TARJETA,device=pinPad,context=com.synthesis.vtolClientLib.VtolContextRepresentation@6c405e13,error=<null>]
2022-04-19 12:52:04,450 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] Module: crdb
2022-04-19 12:52:04,450 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] Message Type: Sale
2022-04-19 12:52:04,454 INFO  [ValidateVtolCrDbSaleMessageReadCardRule] [Thread-0] Executing: class cl.com.synthesis.vtol.clientTbk.business.rules.ValidateVtolCrDbSaleMessageReadCardRule
2022-04-19 12:52:04,455 INFO  [ValidateVtolCrDbSaleMessageReadCardRule] [Thread-0] Validating Read Card data
2022-04-19 12:52:04,455 ERROR [ValidateVtolCrDbSaleMessageReadCardRule] [Thread-0] Error returned by the Pinpad: 99 - Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
2022-04-19 12:52:04,456 INFO  [SendVtolTbkMessageActivityImpl] [Thread-0] ResponseToPosException - ERROR_CONEXION: Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout
2022-04-19 12:52:04,460 INFO  [LibToPosInterpreter] [ApacheWorkerThread-0] Response message: {1:075;2:90;1010:1650383514468;1027:099;1028:Cancelacion del Comando a Traves de la tecla [CANEL] / Timeout;25:20220419125154}
2022-04-19 12:52:04,502 INFO  [TcpIpCommunication] [VtolLibService] Accepting socket from ip: 127.0.0.1 - port: 65378 - soTimeOut: 180000
2022-04-19 12:52:04,504 INFO  [PosToLibInterpreter] [ApacheWorkerThread-0] Request: {1008:CANCEL;2:90;1:075;11:closeSession}
2022-04-19 12:52:04,504 INFO  [IntegrationApi] [ApacheWorkerThread-0] Closing SESSION: RollbackSession
2022-04-19 12:52:04,504 INFO  [EventManager] [Thread-0] Closing session
2022-04-19 12:52:04,504 INFO  [JavaBC] [Thread-0] Close session
```

----

#KAS_Vina_del_Mar_049 - 192.2.49.244
Ultima Venta ABC: 01 Abril | Ultima Venta Webpay: nunca	 

No hay acceso vía Red para revisar