
#Cierre de Lote Requerido

Se ha detectado que esto sucede porque el Kiosko no logra identificar el código de comercio que le corresponde. Según el workaround que se ha encontrado actualmente, se debe solicitar a Raul Diaz que realice el reinicio del Kiosko a nivel de Sistema Operativo.


```
2022-04-05 16:47:10 ERROR VtolClient:616 - Caught event

java.lang.Exception: 718:Cierre de lote requerido debido a cambio de moneda

    at cl.acid.abcdin.transaction.VtolClient.checkResponseCode(VtolClient.java:299) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]

    at cl.acid.abcdin.transaction.VtolClient.authorization(VtolClient.java:195) ~[vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]

    at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:608) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]

    at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]

    at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]

    at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]

    at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]

    at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:781) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
```
 
----

#CSI no encripta 
Este erro sucede cuando luego de reunir la información para enviar el mensaje hacia CSI, el Kiosko intenta encriptar la data y no lo logra, resultando con información con campos NULL y luego el sistema arroja el mensaje de "Sistema Fuera de Servicio". Esto se escala con Raul Diaz, quién aplica mitigación.




```
2022-04-01 16:16:19 INFO  CSI:189 - Plain Request GETKEKAUT: <?xml version='1.0' encoding='ISO-8859-1'?><request_auth>
<service_id>GETKEKAUT</service_id>
<subtype_service>00CSK1001601</subtype_service>
<pan>2022040116161910016</pan>
<ctype>CC</ctype>
<ctext>WKPINAUT10016</ctext>
<interface_id>CMDCSI</interface_id>
<customer_id>K1001601</customer_id>
<client_ip>192.2.16.101</client_ip>
</request_auth>
2022-04-01 16:16:19 INFO  CSI:203 - Encrypted Request GETKEKAUT: <?xml version='1.0' encoding='ISO-8859-1'?><request_auth>
<service_id>GETKEKAUT</service_id>
<subtype_service>00CSK1001601</subtype_service>
<pan>null</pan>
<ctype>null</ctype>
<ctext>null</ctext>
<interface_id>null</interface_id>
<customer_id>null</customer_id>
<client_ip>null</client_ip>
</request_auth>
2022-04-01 16:16:19 ERROR VtolClient:519 - null
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
2022-04-01 16:16:19 ERROR VtolClient:616 - Caught event
java.lang.Exception: El sistema se encuentra fuera de servicio
    at cl.acid.abcdin.transaction.VtolClient.onTransaction(VtolClient.java:520) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
    at cl.acid.abcdin.websocket.Server.onMessage(Server.java:75) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
    at org.java_websocket.server.WebSocketServer.onWebsocketMessage(WebSocketServer.java:524) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
    at org.java_websocket.WebSocketImpl.decodeFrames(WebSocketImpl.java:417) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
    at org.java_websocket.WebSocketImpl.decode(WebSocketImpl.java:170) [vtol-bridge-flow-1.0.0-SNAPSHOT.jar:?]
    at org.java_websocket.server.WebSocketServer$WebSocketWorker.run(WebSocketServer.java:78
```
