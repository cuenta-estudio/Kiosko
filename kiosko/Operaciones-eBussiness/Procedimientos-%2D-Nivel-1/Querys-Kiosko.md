| PROCESO | Querys Kiosko - RDS |
|--|--|
|  AUTOR| @<17962A48-91CA-6013-93A7-25B88797E017>  |


[[_TOC_]]

----

### **Resumen** 
:radio: Se adjuntan a continuación un listado de Querys que serán de ayuda para Análisis y Reportería, correspondiente al Producto Digital Kiosko.


----

Info Adicional:


| *Status OC Kiosko* |
|--|
| 0 = Creada |
| 1 = Carro_Checkout |
| 2 = Pago |
| 3 = Pagado con exito |
| 4 = Cancelado |
| 5 = Cancelado con error |

----

###Accesos RDS

Host: abcdin-appmovil-kiosko-prod.clnvmtbixwtd.us-east-2.rds.amazonaws.com
Puerto: 5432
Database: abcdinappmkiosko

----

#Querys

##Nivel1

###Reporte Stock Kiosko

_select sku as "SKU", app_scope as "blacklist",created_at "Fecha Creación"
from forbidden_products ;_

----

###Reporte para cuadratura Tlogs Kiosko

_select o.folio as "Boleta",o.generated_tlog as "TLOG",o.state as "Status",
o.retail_store_id as "N° Tienda",o.work_station_id as "N° Terminal",o.created_at as "Fecha",
o.bm_transaction_number as "N° Transaccion"
from orders o
inner join order_payments op on o.id = op.order_id
inner join order_shipping_accounts oa on oa.order_id = o.id
where o.created_at between ('2020-05-09 00:00:00') and ('2020-05-10 23:59:00')
and o.state = '3'
order by o.created_at asc ;_

----

###Revisión General Kiosko

_select po.card_type as "TIPO PAGO", o.generated_tlog as "TLOG",o.id as "ORDEN",o.folio as "BOLETA",o.created_at as "FECHA",
o.state as "STATUS", o.total + o.shipping_value as "TOTAL VENTA Regular",po.purchase_total_amount as "TOTAL VENTA Only OFEX", o.shipping_value as "DESPACHO",
o.retail_store_id as "N TIENDA", o.bm_transaction_number as "N° Transaccion", o.address_store as "NOMBRE TIENDA", o.work_station_id as "N° Terminal",
os.rut as "RUT",os.name as "NOMBRE",os.last_name as "APELLIDO",os.phone as "TELEFONO", 
os.address  as "DIRECCION", os.number as "NUMERO",os.depto_home as "DEPARTAMENTO", 
os.region as "REGION", os.district as "COMUNA",op.sku as "SKU", op."name" as "Nombre Producto",
op.quantity as "CANTIDAD COMPRA", op.stock as "STOCK", op.branch_office_code as "BODEGA",
op.normal_total as "Total", op.normal_price as "Price", op.unit_price as "Unit Price", 
op.warranty_price as "Warranty Price",op."document" as "TIPO DESPACHO"
from orders o
inner join order_shipping_accounts os on os.order_id = o.id
inner join order_products op on op.order_id = o.id
inner join order_payments po on po.order_id = o.id
where 1=1
--- Buscar por BOLETA ---
and o.folio in ('17348301')
--- Buscar por OC --
--and o.id in ()
--- Buscar por STATUS ---
--and o.state = '3'
--- Buscar por FECHA ---
--and o.created_at between ('2020-12-17 00:00:00') and ('2020-12-17 23:59:00')
--and  o.address_store in ('La Ligua')
--- Buscar por Rut ---
--and os.rut in ('121722682')
--- Buscar por SKU ---
--and op.sku in ('1138995')
--- Buscar por Tienda
--and o.retail_store_id in ('167')
order by o.id desc;_

----

###Datos Transaccion de Venta
_select o.id as "ORDEN",o.created_at as "FECHA",o.folio as "BOLETA", o.state as "STATUS", o.retail_store_id as "N° TIENDA",
o.address_store as "NOMBRE TIENDA", o.work_station_id as "N° Terminal", op.card_type as "TIPO TARJETA", op.value_process_flow as "TIPO PAGO",
op.purchase_total_amount as "COBRO REALIZADO", op.cic_code_authorization as "CIC", op.tbk_authorization as "CODIGO TBK", op.tbk_bin as "Identificador",
op.voucher as "VOUCHER", op.vtol_trx_id as "TRX",op.account_number as "NUMERO CUENTA", op.card_number as "NUMERO TARJETA", 
op.owner_name as "TITULAR", op.quotes_quantity as "CUOTAS", op.data_origin as"Tarjeta", op.card_type as "TIPO PAGO"
from orders o
inner join order_payments op on op.order_id = o.id
where 1=1
--- Buscar por BOLETA ---
--and o.folio in ('102230686')
--- Buscar por STATUS ---
and o.state = '3'
--- Buscar por FECHA ---
--and o.updated_at between ('2019-07-24 00:00:00') and ('2019-07-24 23:59:00')
and o.retail_store_id in ('093')
order by o.id desc;_

----

###Revisión de Precios

_select PO.file_log_id, PP.product_price_id, PO.shop_code as "Tienda", PO.sku as "SKU", PO.normal as "Precio Normal", PP.price as "Precio Vigente",
PP.date_from as "Fecha Inicio", PP.date_to as "Fecha Fin", PP.created_at as "Creacion Precio Vigente", PP.updated_at as "Update Precio Vigente"
from product_prices PO
inner join product_promotions PP on PO.id = PP.product_price_id 
where 1=1
--Busca por ID de Tienda--
and shop_code=10275
--Busca por SKU--
and sku='1100096' ;_

----

###Reporte Ventas con Garantía Extendida

_select o.created_at as "FECHA", o.state as "STATUS", oy.card_type "Tipo Pago",o.id as "ORDEN",o.folio as "BOLETA",
o.retail_store_id as "NÂ° TIENDA", o.address_store as "NOMBRE TIENDA",
os.rut as "RUT", op.sku as "SKU", op."name" as "Nombre Producto", op.quantity as "CANTIDAD COMPRA", 
op.unit_price as "Precio Unidad", o.shipping_value as "DESPACHO", op.warranty_price as "Precio Garantia", o.total + o.shipping_value as "TOTAL VENTA"
from orders o
inner join order_shipping_accounts os on os.order_id = o.id
inner join order_products op on op.order_id = o.id
inner join order_payments oy on oy.order_id = o.id
where 1=1
--- Buscar por BOLETA ---
and o.folio in ('101663709','101639920','101714669')
--- Buscar por OC --
--and o.id in ()
--- Buscar por STATUS ---
--and o.state = '3'
--- Buscar por FECHA ---
--and o.created_at between ('2019-12-24 00:00:00') and ('2019-12-26 23:59:00')
---- Buscar por SKU ---
--and op.sku in ('')
order by o.id desc;_

----

##Nivel 2

###Revisión de Archivos de Carga de Precio

_select * from files_logs where creation_date between ('2020-05-14') and ('2020-05-15');_

_select * from files_logs where state in ('processed');_

_select * from files_logs where state in ('processing');_

_select * from files_logs where state in ('error');_

----

###Revisión Tiendas Habilitadas/Deshabilitadas

_select * from kiosks;_

_select * from kiosks  where store_id in ('10281');_

----

###Revisión Promociones

_select * from price_promotions pp 
inner join order_products op on op.order_id = pp.order_product_id 
where 1=1
and op.sku in ('1133373')
order by created_at desc;_

----

###Revisión Regla de Precios

_SELECT * FROM configuration_price_worker_apps;_

----

###Cambio de Precio por BD

----## Cambiar precio##----
--Primero verificar precio de SKU
_select PO.file_log_id, PP.product_price_id, PO.shop_code as "Tienda", PO.sku as "SKU", PO.normal as "Precio Normal", PP.price as "Precio Vigente",
PP.date_from as "Fecha Inicio", PP.date_to as "Fecha Fin", PP.created_at as "Creacion Precio Vigente", PP.updated_at as "Update Precio Vigente"
from product_prices PO
inner join product_promotions PP on PO.id = PP.product_price_id 
where 1=1
--Busca por ID de Tienda--
and shop_code=10273
--Busca por SKU--
and sku='1144976';_

--Seleccionar el ID para Identificar precios
_select * from product_promotions where product_price_id = 6841153;_

--Update del precio
_update public.product_promotions
set price = 329990
where id = 6841153;_

--Update de Fecha Vigencia
_update public.product_promotions
set date_to = '2020-03-17'
where id = 6841153_

----

###Habilitación de Tienda

_INSERT INTO kiosks (terminal_id,store_id,bm_url,created_at,updated_at,open)
VALUES(20,10411,'http://192.5.11.244:8080/rs-bm-console-rs-bm-kiosco-server-abcdin/ServiceKioscoBean?wsdl',current_timestamp,current_timestamp,'true');_

----

###Usuarios conectados
select * from pg_stat_activity;

----
----















