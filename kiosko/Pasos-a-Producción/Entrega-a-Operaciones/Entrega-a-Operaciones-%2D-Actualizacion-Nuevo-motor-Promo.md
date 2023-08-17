

| Descripción | #18092 |
|--|--|
Build | [CI-RELEASE-kiosko-back](https://dev.azure.com/ADretail/kiosko/_build/results?buildId=1589&view=results)
Build | [CI-RELEASE-kiosko-promo](https://dev.azure.com/ADretail/kiosko/_build/results?buildId=1541&view=results)

[[_TOC_]]

# Conpendio Tecnico

# Contexto

Dada la inclusion del nuevo motor promo, se requiere adicionar nueva informacion en la cabecera del xml que se envia hacia el servidor de Promo.

## Desarrollo

El desarrollo contempla dos modificaciones
- En el Backend se realizara la configuracion del OMR para agregar una nueva columna [new_promo] a la tabla Kioks, al momento de realizar la migracion. Adicionalmente se modifica el Schema, para que al realizar la consulta a la DB se traiga el nuevo campo.

Esta informacion nueva en el kioks, viaja en la cabecera de la request al momento de conectarse hacia kiosko-promo.
- En el Kiosko Promo, se obtiene el valor de este nuevo campo, y en caso que este este activo [valor true] anexa la informacion adicional a la cabezera.

----

### Backend

1. se crea archivo db > migrations > 20201222170133-addNewPromoColumnsInKioskoTable.js , el cual contiene la informacion relacionada al anexo de la nueva columna en la tabla kioks.
2. Se modifica el archivo src > components > kiosks > models.js, en donde se anexa al schema la nueva columna new_promo.

----

### Promo

Se modifico la funcion **buildHeader**, de la clase **Message**, ubicada en src > controllers > message > index.js. En donde se obtiene el valor de new_promo, en caso que sea falso, no se realiza ningun cambio, en caso que sea verdadero se le appenda a la cabecera el tag `@companyId:'abcdin'`

----

## Implementacion

Para aquellos kioskos que se encuentren operando con el antiguo motor de promociones, no se debe realizar ningun cambio.
Para aquellos kioskos con el nuevo motor promo, es necesario que cuando se realice el cambio al nuevo motor, adicionalmente se configure en la base de dato el valor del campo new_promo de la tabla kioks a `true`

![image.png](/.attachments/image-6d69178a-5da8-47ea-ac18-760089688704.png)

----
## -QA

Para aplicar este cambio es necesario cambiar la tabla kiosks, se busca la tienda en la que se requiere probar y se activa(true) el nuevo motor promo (new_promo) y esto se visualiza de la siguiente manera 

![QA new promo true.png](/.attachments/QA%20new%20promo%20true-3e5dd877-7517-496e-a04b-040721062ca0.png)

Y este cambio nos da la siguiente respuesta 

![yyyyyy.png](/.attachments/yyyyyy-bd992a3c-ab66-4122-91e5-4b33de294f73.png)