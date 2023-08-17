| PROCESO | Cuadratura de Ventas Kiosko |
|--|--|
|  AUTOR| @<17962A48-91CA-6013-93A7-25B88797E017>  |


[[_TOC_]]

----

## **Objetivo** 
:dart: En este documento se entregarán algunos tips básicos para la revisión de boletas, directamente desde los servidores de aplicaciones de Kiosko.

----
## **Alcance del procedimiento** 

:information_source: Este procedimiento aplica cómo revisión básica. Tanto para un Nivel 1, como para un Nivel 2 en una primera etapa.

----
 **Check list accesos** :white_check_mark:

- [X] Validar conexión a Servidores de Aplicación

----
## **Procedimiento**

### **Directorios Contenedores**

Nos conectaremos al servidor de aplicaciones, en este caso nos conectamos al App1 o App2.
![image.png](/.attachments/image-716b7e09-d0f4-4d28-8d7b-a50de2e15413.png)

Iremos al siguiente directorio: `/opt/kiosko-back/__appData__`
En donde nos encontraremos con los siguientes sub-directorios:

![image.png](/.attachments/image-2d9e43ae-64cc-46a7-be00-1c59d7b5ab25.png)

- [X] Directorio _boleta_: Aquí encontraremos todas las boletas que se generan en Kiosko. Este archivo es un txt, en donde su encabezado mantiene el número de boleta, la fecha de generación y la hora en que se generó la compra.

![image.png](/.attachments/image-530ef80b-bdea-4507-ae77-8d54954b7376.png)

- [X] Directorio _tlog_:  Aquí encontraremos los XML generados de cada documento. Los cuales vienen con el código TX que identificaremos luego en la boleta.

![image.png](/.attachments/image-41e11217-9584-43aa-b5b9-6948e5751f3c.png)

- [X] Directorio _voucher/cic_: En estos directorios encontraremos los vouchers que se generan, en caso de que la compra haya sido vía Transbank o Abcdin. Estos archivos también vienen en formato txt.

![image.png](/.attachments/image-d55f7bec-ef73-4540-ba8b-7947e5b793a7.png)

![image.png](/.attachments/image-5f6539fe-ed04-4ba5-a327-03c9a0c34268.png)

### **Documentos Asociados a la Venta**

- [X] Archivo Boleta*.txt
Si revisamos el archivo de una boleta, podremos ver la boleta tal cual la recibe el cliente final.

![image.png](/.attachments/image-ea049841-f92a-433e-9a93-774a8a388486.png)

En este documento, los puntos a considerar son los siguientes:

- **Numero de Boleta**: Este es el número de documento, el cual se genera al momento de enviar un producto al carro de compras.
- **TX:** Esto nos dará el nombre del archivo xml.
- **Tienda:** Especifica el número de la sucursal, en donde 10 es un código por defecto, los siguientes números corresponden a la sucursal. En este caso la sucursal es la 613.
- **Caja:** Corresponde al Módulo Kiosko en el cual se realiza la compra. Normalmente es 20 o 21.
- **Fecha:** Especifica la fecha en que se realizó la compra.

**Estos son los datos precisos que necesitamos al momento de buscar una boleta en el S3.**

![image.png](/.attachments/image-a81f67b6-bc77-4042-8385-7555326e24a7.png)

- [X] Archivo TLOG
Si revisamos un archivo XML generado, podremos ver todos los datos asociados a la compra del producto. Desde los datos del cliente, hasta el método de pago.

Este xml ordena todos los datos y viajará . Esta es la información que será validada para ingresarla a todos los sistemas contables. Es de vital importancia que este archivo se genere, para que llegue a contabilidad.

![image.png](/.attachments/image-4e61bf6c-df54-4f86-ac5f-81640e116b22.png)
_<?xml version="1.0"?>
<POSLog xmlns:lxslt="http://xml.apache.org/xslt">
  <Transaction CancelFlag="false" TrainingModeFlag="false" SuspendedFlag="false" VoidedFlag="false" OfflineFlag="false">
    <RetailStoreID>645</RetailStoreID>
    <DirecStore>Talca</DirecStore>
    <CityStore>Santiago</CityStore>
    <CmnaOrigen/>
    <WorkstationID>20</WorkstationID>
    <TillID>4</TillID>
    <TillType>Workstation</TillType>
    <SequenceNumber>1276</SequenceNumber>
    <BusinessDayDate>2020-11-02</BusinessDayDate>
    <Period>5753</Period>
    <Subperiod>5754</Subperiod>
    <BeginDateTime>2020-11-02T17:49:54</BeginDateTime>
    <EndDateTime>2020-11-02T17:49:54</EndDateTime>
    <OperatorID>143978613</OperatorID>
    <OperatorName/>
    <OriginalTransaction>null</OriginalTransaction>
    <EnterpriseCode>00001</EnterpriseCode>
    <RetailTransaction Version="2.2">
      <DocumentType>BOL</DocumentType>
      <DocumentGenerationType>AUT</DocumentGenerationType>
      <DocumentNumber>102982886</DocumentNumber>
      <DocumentStatus>VIG</DocumentStatus>
      <SaleType>TRA</SaleType>
      <IdentificadorUnico>064500002020110205495433</IdentificadorUnico>
      <StatusTransmision>ONLINE</StatusTransmision>
      <CalculatorID>20110205473333</CalculatorID>
      <GenericCustomerFlag>true</GenericCustomerFlag>
      <Customer>
        <LastName>VALLADARES</LastName>
        <MotherLastName>AVILA</MotherLastName>
        <FirstName>XIMENA</FirstName>
        <SecondName>DEL PILAR</SecondName>
        <PhoneCode/>
        <PhoneNumber/>
        <PhoneType/>
        <PhoneLocation/>
        <Email/>
        <Category>INA2</Category>
        <Type>1</Type>
        <RUT>14.564.847-5</RUT>
        <State>MAULE</State>
        <StateCode>2390</StateCode>
        <City>TALCA</City>
        <CityCode>7</CityCode>
        <District>TALCA</District>
        <DistrictCode>7</DistrictCode>
        <Address>PASAJE TREINTA 1/2 ORIENTE 3073</Address>
        <CustomerType>0</CustomerType>
      </Customer>
      <LineItem EntryMethod="Keyed">
        <SequenceNumber>1</SequenceNumber>
        <Sale>
          <ItemID>1136442</ItemID>
          <ItemIDdv>1136442-k</ItemIDdv>
          <ItemDesc>Cama Europea Celta 1,5 Plazas Evolution Black +...</ItemDesc>
          <ItemType>1</ItemType>
          <MerchandiseHierarchy>106</MerchandiseHierarchy>
          <Quantity Units="" UnitOfMeasureCode="UN">1</Quantity>
          <RegularSaleUnitPrice>123990</RegularSaleUnitPrice>
          <TotalDiscountLine>7000</TotalDiscountLine>
          <ExtendedAmount>116990</ExtendedAmount>
          <Tax TaxType="VAT" TypeCode="Sale">
            <SequenceNumber>1</SequenceNumber>
            <TaxAuthority>IVA 19%</TaxAuthority>
            <Amount>19797</Amount>
            <TaxableAmount TaxIncludedInTaxableAmountFlag="true">104193</TaxableAmount>
            <Percent>19</Percent>
          </Tax>
          <ItemStatus>VIG</ItemStatus>
          <WarrantableFlag>true</WarrantableFlag>
          <WarrantySold/>
          <CostUnitPrice>98793</CostUnitPrice>
          <Shipment>
            <Type>SP</Type>
            <RetailStoreSource>50159080</RetailStoreSource>
            <DueDate>2021-01-13</DueDate>
            <State>MAULE</State>
            <StateCode>7</StateCode>
            <City>Talca</City>
            <CityCode>2390</CityCode>
            <District>Talca</District>
            <DistrictCode>2390</DistrictCode>
            <Address>19 ote 5 sur</Address>
            <AddressNumber>701</AddressNumber>
            <RetailStoreTarget>645</RetailStoreTarget>
            <Serial>45810</Serial>
            <FirstName>ximena</FirstName>
            <SecondName/>
            <LastName>valladeres</LastName>
            <MotherLastName>avila</MotherLastName>
            <Phone1Code>+56</Phone1Code>
            <Phone1Number>933709066</Phone1Number>
            <Phone2Code/>
            <Phone2Number/>
            <Observacion>llamar antes</Observacion>
          </Shipment>
          <CICItemAdditionalData>
            <ItemCode>1136442</ItemCode>
            <UnitPrice>123990</UnitPrice>
            <Quantity>1</Quantity>
            <TotalAmount>123990</TotalAmount>
            <ToFinanciate>116990</ToFinanciate>
            <ItemRate>0</ItemRate>
            <FeeAmount>116990</FeeAmount>
            <RescueValue>116990</RescueValue>
            <RateType>N</RateType>
          </CICItemAdditionalData>
          <SellerId>143978613</SellerId>
          <SellerTy/>
          <RetailPriceModifier MethodCode="PM">
            <SequenceNumber>1</SequenceNumber>
            <Amount Action="SB">7000</Amount>
            <FirstPurchase>false</FirstPurchase>
            <ReasonCode>PM</ReasonCode>
            <PrinterPromotion>25441</PrinterPromotion>
            <WorkerID/>
            <PromotionName>25441</PromotionName>
            <PivotalCampaignNumber/>
            <ModifierReason/>
          </RetailPriceModifier>
        </Sale>
      </LineItem>
      <LineItem EntryMethod="Keyed">
        <SequenceNumber>2</SequenceNumber>
        <Sale>
          <ItemID>111161</ItemID>
          <ItemIDdv>111161-2</ItemIDdv>
          <ItemDesc>FLETE</ItemDesc>
          <ItemType>4</ItemType>
          <MerchandiseHierarchy>106</MerchandiseHierarchy>
          <Quantity Units="" UnitOfMeasureCode="UN">1</Quantity>
          <RegularSaleUnitPrice>11990</RegularSaleUnitPrice>
          <TotalDiscountLine/>
          <ExtendedAmount>11990</ExtendedAmount>
          <Tax TaxType="VAT" TypeCode="Sale">
            <SequenceNumber>2</SequenceNumber>
            <TaxAuthority>IVA 19%</TaxAuthority>
            <Amount>1914</Amount>
            <TaxableAmount TaxIncludedInTaxableAmountFlag="true">10076</TaxableAmount>
            <Percent>19</Percent>
          </Tax>
          <ItemStatus/>
          <WarrantableFlag>false</WarrantableFlag>
          <WarrantySold/>
          <CostUnitPrice/>
          <SellerId>143978613</SellerId>
          <SellerTy/>
        </Sale>
      </LineItem>
      <LineItem>
        <SequenceNumber>3</SequenceNumber>
        <Tender TenderType="cDIN" TypeCode="Sale">
          <Amount>128980</Amount>
          <IVAICA>DF19</IVAICA>
          <FinanciationOWType>TCD</FinanciationOWType>
          <FinanciationPlan>2</FinanciationPlan>
          <StoreAccount>
            <AuthorizationCode>4757163</AuthorizationCode>
            <AuthorizationType/>
            <VoucherNumber>8102982886</VoucherNumber>
            <AccountNumber>4003028413</AccountNumber>
            <AuthorizationDate>2020-11-02</AuthorizationDate>
            <StartSessionDate>2020-11-02</StartSessionDate>
            <SessionID>2020110216452014397861311111</SessionID>
            <CardNumber>4946113162336002</CardNumber>
            <EnterpriseCode>1</EnterpriseCode>
            <Origin>IC</Origin>
            <FlowValue>ABCVISA</FlowValue>
            <TrxNumber>655536</TrxNumber>
          </StoreAccount>
          <CICTenderAdditionalData>
            <FeeValue>128980</FeeValue>
            <RescueValue>128980</RescueValue>
            <AVMValue>0</AVMValue>
            <MediaCICRate>0</MediaCICRate>
            <FactorDesfase>1</FactorDesfase>
            <DiasDesfaseCobrados>0</DiasDesfaseCobrados>
            <FeeQuantity>1</FeeQuantity>
          </CICTenderAdditionalData>
          <ForeignCurrencyAmount>0</ForeignCurrencyAmount>
          <EmitterRUT/>
          <CreditDebitCardData>
            <CardNumber/>
            <AuthorizationID/>
            <UniqueNumber/>
          </CreditDebitCardData>
          <AuthorizationType>M</AuthorizationType>
          <NumberOfInstallments>1</NumberOfInstallments>
          <AccountNumber>4003028413</AccountNumber>
          <SerialNumber>8102982886</SerialNumber>
          <ExpirationDocumentDate>2020-12-10</ExpirationDocumentDate>
        </Tender>
      </LineItem>
      <Total TotalType="TotalItemSale" CancelFlag="false">2</Total>
      <Total TotalType="TransactionGrossPositiveAmount" CancelFlag="false">135980</Total>
      <Total TotalType="TransactionGrossNegativeAmount" CancelFlag="false">0</Total>
      <Total TotalType="TransactionTaxAmount" CancelFlag="false">21711</Total>
      <Total TotalType="TransactionManualDiscount" CancelFlag="true">0</Total>
      <Total TotalType="TransactionAutomaticDiscount" CancelFlag="true">7000</Total>
      <Total TotalType="TransactionAmountNeto" CancelFlag="false">114269</Total>
      <Total TotalType="TransactionAmountTotal" CancelFlag="false">128980</Total>
      <Total TotalType="GlosaAmountTotal" CancelFlag="false">CIENTO VEINTIOCHO MIL NOVECIENTOS OCHENTA PESOS CHILENOS </Total>
    </RetailTransaction>
  </Transaction>
</POSLog>_

- [X] Archivo TBK*.txt // ABC*.txt
Si revisamos los archivos que se encuentran en los directorios voucher y cic encontraremos los vouchers correspondientes a Transbank y AbcVisa. Los cuales figuran de la siguiente manera y viene codificada:

**Voucher Transbank**
![image.png](/.attachments/image-dca52ba5-0a4e-485c-9dbf-e483bc472b40.png)

si necesitamos revisar el voucher por línea de comandos, podemos ver el contenido de este mensaje con la siguiente sintaxis:

`echo 'mensaje a decodificar' | base64 --decode`

![image.png](/.attachments/image-60771c9b-8885-4009-b492-07a68c85472e.png)

![image.png](/.attachments/image-d49b80f6-049b-4494-b3c9-7077077414c9.png)

**Voucher ABC**

![image.png](/.attachments/image-385791fe-682f-4429-9886-0ec4009d6bf0.png)

###**Comandos de Búsqueda**
Si necesitamos buscar una boleta y validar que se hayan generado todos los archivos correspondientes, realizaremos los siguientes pasos.

Nos situamos en el siguiente directorio: `/opt/kiosko-back/__appData__`

Podemos ejecutar el siguiente comando:
`grep -ri Número de Boleta ./`

Con este comando podremos ver cualquier archivo que contenga el número de boleta a buscar, se mostrará todas las veces que se mencione esta boleta.

![image.png](/.attachments/image-e8703290-ee95-432d-a467-26146dd084d6.png)
Nota: Al encontrarse codificado el voucher, no aparecerá en esta vista.

Ya con esta información, podemos:
- Validar que existe boleta y revisar los datos de la misma
- Validar que se hayan generado TLOG.
- Validar información para revisar en S3

Otra forma de buscar sería el siguiente comando (en el mismo directorio inicial): 

`find . -name *Número de Boleta*`

El cual nos mostrará cualquier archivo que tenga el valor buscado, sin embargo como veremos a continuación, esto solo nos entrega 2 achivos y su directorio. Ya que el XML no tiene el número de boleta en el encabezado del archivo, pero aquí si podemos validar el Voucher, esto porque el documento contiene el número de la boleta en su encabezado. 
Por lo tanto, la manera aquí sería validar los 2 archivos, identificar el TX en la boleta y luego buscar el archivo correspondiente al xml en su directorio correspondiente.

![image.png](/.attachments/image-95c3c3b1-a72b-413d-afcb-ccfe11314319.png)

Hasta este punto ya hemos podido validar:
- Boleta
- Voucher
- Tlog

Así también, hemos podido realizar una revisión básica de los archivos generados para una boleta en el Servidor de Aplicaciones.