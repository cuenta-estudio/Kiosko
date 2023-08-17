| PROCESO | Cuadratura de Ventas Kiosko |
|--|--|
|  AUTOR| @<17962A48-91CA-6013-93A7-25B88797E017>  |


[[_TOC_]]

----

### **Objetivo** 
:dart: El objetivo de este procedimiento es realizar un cuadre de las ventas efectivas en el producto digital Kiosko, contrastado con los sitemas de Backoffice.
_Cuando nos referimos al BackOffice, hablamos del sistema de despacho (SDD) y los sistemas de Retail._

----
### **Info** 

:information_source: A lo que Kiosko refiere, debemos entender que al momento de generarse la venta efectiva (status 3 en Kiosko) se genera un xml con todos los datos de la venta, el cual llamamos TLOG. Una vez generado el TLOG, este xml viaja a SDD para generar el despacho y a su vez viaja al BM, el cual validará este formato xml y pasará a los esquemas de retail (Retail1 - Retail2 - JDE).

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

----
 **Check list accesos** :white_check_mark:

- [X] Validar conexión RDS
----
### **Recolección de Data** 

:bookmark_tabs:  Para realizar este cuadre utilizaremos el siguiente template:
[Reporte Cuadratura Kiosko.xlsx](/.attachments/Reporte%20Cuadratura%20Kiosko-496d12ba-c21c-46ad-8aa5-58d247fc8e12.xlsx)

Adicionalmente se requerirá de la información proveniente de los sistemas del BackOffice, data que se genera por parte del equipo de Explotación de Datos y nos llega vía correo diariamente:
**SDD:**
![image.png](/.attachments/image-4713824f-beba-4491-9c54-3af9c0abb5b6.png)

**Esquemas de Retail:**
![image.png](/.attachments/image-d00e1833-c4c6-4e01-abec-8773bb301963.png)

----
----
### **Procedimiento** 

:memo: Como primer paso procedemos a conectarnos al RDS (Base de Datos Kiosko) y ejecutaremos la siguiente Query:


#### Query Cuadratura Kiosko ####
_SELECT o.folio as "Boleta",o.generated_tlog as "TLOG",o.state as "Status",
o.retail_store_id as "N° Tienda",o.work_station_id as "N° Terminal",o.created_at as "Fecha",
o.bm_transaction_number as "N° Transaccion"
FROM orders o
INNER JOIN order_payments op on o.id = op.order_id
INNER JOIN order_shipping_accounts oa on oa.order_id = o.id
WHERE o.created_at between ('2020-05-09 00:00:00') and ('2020-05-10 23:59:00')
AND o.state = '3'
ORDER BY o.created_at ASC ;_

#### Recolección de Data ####

:floppy_disk: Exportaremos esta data y la llevaremos al Template "Reporte Cuadratura Kiosko" a la pestaña _BASE_KIOSKO_.
![image.png](/.attachments/image-eeccb831-4f77-47db-9c87-46b349a49a60.png)

Exportamos el reporte de los Esquemas de Retail (correo "información Cuadratura Kiosko") y lo adjuntaremos a la pestaña _BACKOFFICE_.
![image.png](/.attachments/image-eb9067b8-ecab-4d6b-acf3-a51c836afb9d.png)

Realizaremos la misma tarea con la información generada de SDD (correo "sdd kiosko") y adjuntaremos la data en la pestaña _SDD_.
![image.png](/.attachments/image-1ccfd8a7-fb50-47d8-9a33-2a35fb511341.png)

Con toda esta data recolectada, iremos a la pestaña _CUADRE_, la cual contiene fórmulas preseteadas.
En esta pestaña copiaremos el listado completo de boletas desde la pestaña _BASE KIOSKO_, seleccionaremos  desde la columna B a la H y aplicaremos estas fórmulas hasta la última boleta.
![image.png](/.attachments/image-ca130ada-654e-4cfa-8e6c-1e560e09224e.png)

![image.png](/.attachments/image-98dad687-1bba-4254-95e8-fa2e4f0c681b.png)

Una vez realizada esta tarea, vamos a la pestaña _INFORME_, el cual contiene la tábla dinámica que resume toda la información recolectada.

En esta pestaña haremos click en la tabla dinámica y agregaremos la información a considerar, la cual será información de la pestaña _CUADRE_.
![image.png](/.attachments/image-c1ef3b6d-47a8-42cb-8233-d0e0ef770ffc.png)

![image.png](/.attachments/image-e3113ca8-3ea5-47c9-a2db-b00b178a43b5.png)

#### Tabla Dinámica ####

:chart_with_upwards_trend::chart_with_downwards_trend: Una vez hagamos click en "Aceptar", para asegurarnos de que la tabla contenga la data actualizada, con esta misma seleccionada, actualizaremos.
![image.png](/.attachments/image-2e5d8cf5-9c55-477d-bd8e-d3b7a73de6a3.png)

Al actualizar veremos la tabla con la información necesaria.
![image.png](/.attachments/image-96fb72be-bf7f-4d94-bbc6-4229f3efa4f8.png)

#### Comunicación a Stakeholders ####

:loudspeaker: Ya con esta información se procederá a enviar la comunicación vía Correo a los stakeholders, bajo el siguiente formato y adjuntando el excel.
![image.png](/.attachments/image-40212047-b1bd-4a58-b1d4-d8266050bc59.png)

A continuación se adjunta un caso en el cual se detectan descuadres:
![image.png](/.attachments/image-1d4506a2-1b8b-46ff-af3f-1112c0633992.png)

:warning:**Importante**:warning: 

Es de vital importancia que antes de enviar la comunicación, se generen los tickets de incidentes relacionados a cada caso con descuadre. Esto para generar la mitigación del caso y ser comunicado en este mismo correo.

----
----
###**Mitigación de Casos**

:hourglass_flowing_sand: A continuación se adjunta un esquema para la mitigación de los casos con descuadre en Kiosko.

| Tipo Descuadre | Se recupera venta | Responsable | Acción Nivel 1 |
|--|--|--|--|
| Cobro Efectivo - OK TLOG - OK SDD - NO BM | Si | Explotación de Datos | Enviar TLOG a Explotación para Reinyección del TLOG en BM |
| Cobro Efectivo - OK TLOG - NO SDD - NO BM | Si | Explotación de Datos | Enviar TLOG a Explotación para Reinyección del TLOG en los sistemas de BO |
| Cobro Efectivo - OK TLOG - NO SDD - OK BM | Si | Explotación de Datos | Enviar TLOG a Explotación para Reinyección del TLOG en SDD |
| Cobro Efectivo - NO TLOG - NO SDD - NO BM | Si | Explotación/Ops eBussines | Ejecutar procedimiento de regeneración de TLOG y enviar TLOG a Explotación para reinyección en los sistemas de BO |
| Cobro Efectivo con Reversa Aplicada - OK TLOG - OK SDD - NO BM | No | Operaciones eBussines | Anulación de Venta vía Auris| Tbk: "Contabilidad" - ABC: "Mantención de Cuentas" |
| Cobro Efectivo con Reversa Aplicada - OK TLOG - NO SDD - NO BM | No | Operaciones eBussines | Anulación de Venta vía Auris| Tbk: "Contabilidad" - ABC: "Mantención de Cuentas" |
| Cobro Efectivo con Reversa Aplicada - NO TLOG - NO SDD - NO BM | No | Operaciones eBussines | Anulación de Venta vía Auris| Tbk: "Contabilidad" - ABC: "Mantención de Cuentas" |



