Los diagrama a continuación solo refleja las iteraciones sus componente  a medida que avance el analisis, se detallara las secuencias correspondientes, estos se dividen en:

[[_TOC_]]


## Diagrama Totem
> diagrama de los elemento/componentes que participan en dentro del totem en cada tienda


::: mermaid
 sequenceDiagram
    %%autonumber 
    participant brs as browser
    participant aws as aws
    participant exe as java app
    participant vtlb as vtol brige
    participant vtlc as vtrol client
    participant print as impresora
    participant pos as pos

     note over brs : browser electronjs      
    brs ->> aws : http://app.abcdin.cl
     note over exe : aplicacion consola
    exe ->> vtlb: interacion adminstracion pos
    exe ->> vtlc: interacion con sistema pos
    exe ->> print: imprimir boleta
    brs ->> pos: accion venta
:::

## Diagrama AWS
> diagrama de los elemento/componentes que son principalmente desplegados dentro de aws

::: mermaid
 sequenceDiagram
    %% autonumber 
    participant ngx as nginx
    participant front as front-end
    participant back as back-end
    participant redis as redis
    participant db as rds postgres
    participant wp as worker prices
    participant wc as worker categories
    participant ftp as ftp
    participant ecom as ecom
 
    note over ngx: balanceador <br/> appServer 1 <br/>appServer 2
    opt appserver 1 & appserver 2
         note over front: web reactjs
        ngx->>front: aplicacion web
         note over back: back nodejs
        front->>back: aplicacion back
    end
    opt database
         note over redis: cache 
        back->>redis: cache catalogo-precios-stock
         note over db: servicio aws db
        back->>db: base de datos de la app
    end
    opt worker
         note over ftp: ftp adretail
        wp->>ftp: archivo precios
        ftp-->>wp: carga archivo
        wp->>db:inserta precios
         note over ecom: ecom magento
        wc->>ecom: servico de categorias ibm ecom 
        ecom-->>wc: retorna categorias
        wc->>redis: actualiza cache categorias
    end
:::

## Diagrama BackEnd/BackOffice
> diagrama de los elemento/componentes que interactúan entre aws y backend/backoffice adretail

::: mermaid
 sequenceDiagram
    %% autonumber 
    participant kiok as kiosko
    participant ecom as ecom
    participant milli as milleway
    participant pmm as pmm
    participant bmt as bmtienda
    participant sdd as sdd
    
    

    kiok->>ecom: consulta stock/categorías
    kiok->>milli: Calculadora/Agendamiento
    kiok->>pmm: Confirma disponibilidad stock
    kiok->>bmt: Comunicación con Tienda Física/ Genera trasaccion venta pos
    kiok->>sdd: Confirma Despacho
    
   
:::
