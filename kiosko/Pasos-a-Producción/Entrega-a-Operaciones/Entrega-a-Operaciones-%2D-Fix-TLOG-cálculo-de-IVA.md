Historia: 
HU #3653

[[_TOC_]]

----
#Compendio Técnico


_A continuación se informan los siguientes cambios realizados a nivel de Desarrollo._

----
##Desarrollo
### Backend

Proyecto: **kiosko-back**
1. Se modifica el archivo `src/middlewares/tlog/formatTlogJson.js`
2. Los cambios se aplican al método `buildRetailPriceModifier()` donde se valida la promoción y el medio de pago de la compra.
3. Si el artículo tiene promoción se toma el valor de "value" y se le resta al precio regular del producto. Si "value" es NULL y el tipo de promoción es _PercentageDiscount_ entonces se toma el valor de "percent" y se descuenta ese porcentaje del precio regular del producto.
4. Los cambios en el TLOG se aplican solo si el medio de pago es ABCVisa.

**Implementación**


```
const buildRetailPriceModifier = (item, promo, index) => {
      log.debug('<<< buildRetailPriceModifier >>>');

      if (promo === null) {
        return null;
      }

      let extendedAmount = 0;
      const percentPromo = percentTlogTag(promo);
      if (percentPromo) {
        const promoAmount = promo.get('value')
          ? promo.get('value')
          : Math.round(item.get('unit_price') * (promo.get('percent') / 100));
        extendedAmount = item.get('unit_price') - promoAmount;
      } else {
        extendedAmount = item.get('unit_price') - promo.get('value');
      }

      const netoWithDecimals = parseFloat(extendedAmount) / 1.19;
      const neto = Math.round(netoWithDecimals);
      const iva = Math.round(extendedAmount - netoWithDecimals);

      const priceModifier = {
        ExtendedAmount: extendedAmount * item.get('quantity'),
        Tax: {
          '@TaxType': 'VAT',
          '@TypeCode': 'Sale',
          SequenceNumber: index + 1,
          TaxAuthority: 'IVA 19%',
          Amount: iva * item.get('quantity'),
          TaxableAmount: {
            '@TaxIncludedInTaxableAmountFlag': true,
            '#text': neto * item.get('quantity'),
          },
          Percent: 19,
        },
        RetailPriceModifier: {
          '@MethodCode': 'PM',
          SequenceNumber: index + 1,
          Amount: {
            '@Action': 'SB',
            '#text': promo.get('value'),
          },
          ...percentPromo,
          FirstPurchase: false, // This value can change when we start using info from conInfoCuenta 3 in the promo feature
          ReasonCode: 'PM',
          PrinterPromotion: promo.get('id'), //  promo ID
          WorkerID: '',
          PromotionName: promo.get('id'), // promo ID
          PivotalCampaignNumber: '',
          ModifierReason: '', // Blank value always by definition
        },
      };

      return item.card_abc_price && order.order_payment.get('card_type') === 'ABC'
        ? priceModifier
        : null;
    };
```


----

#Documentación Operaciones
A continuación se entregará información relevante de acuerdo a las modificaciones realizadas, correspondiente a la Operación. 

##Validaciones

Al visualizar los Tlog se valida que:
<TaxableAmount TaxIncludedInTaxableAmountFlag="true"> sea igual a <ExtendedAmount> /1 + <Percent>19</Percent> /100
Esto se puede observar en el Tlog de la siguiente manera 
 
![i i 1.png](/.attachments/i%20i%201-c6c7b63e-0df6-4ab0-bd4a-44610f7475c6.png)

Y también se valida que <Amount> es igual a <ExtendedAmount>     -     <TaxableAmount TaxIncludedInTaxableAmountFlag="true">
Esto se muestra en el Tlog de la siguiente manera
![ii 2.png](/.attachments/ii%202-af52e23a-c693-4008-b69d-fc733219ee6a.png)


----
##Manual Técnico Paso a Producción
El Paso a Producción se estará llevando a cabo mediante el siguiente documento Técnico, en los servidores de Aplicación:

[Manual Tecnico Paso a Producción Back End](https://dev.azure.com/ADretail/kiosko/_wiki/wikis/kiosko.wiki/283/Manual-T%C3%A9cnico-Paso-a-Producci%C3%B3n-Back-End)