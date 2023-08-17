investigación para solucionar incidente #170

::: mermaid
graph LR;
    USER(Totem)-->I(internet);
    USER-->E(ethernet);
    I-->|104.17.75.14|C(cloudflare);
    C-->APP(app.abcdin.cl);    
    E-->|13.58.193.233|APP;
:::
::: mermaid
graph LR;
    USER(Totem)-->I(internet);
    USER-->E(ethernet);
    I-->|104.17.75.14|C(cloudflare);
    C-->APP(abcdin.cl);    
    E-->|169.54.216.28|APP;
:::


>servicio catalogo
'https://www.abcdin.cl/wcs/resources/store/10001/productview/bySearchTerm/6?pageNumber=1&pageSize=50'

>img catalogo producto
'https://www.abcdin.cl/wcsstore/ABCDIN/images/led/1130279F13.jpg'

---
>cloudflare vs ethernet

`se aprecia diferencia entre navegacion por internet publica vs red interna con trafico aislado`
![2020-03-11_13-28-13.png](/.attachments/2020-03-11_13-28-13-ed03f4de-b651-40bd-bd00-32383f137561.png)

---
>**json structure**
<DIV style="color: #e6e6e6;background-color: #292a2b;font-family: Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre"><DIV><SPAN style="color: #e6e6e6">{</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;</SPAN><SPAN style="color: #ffcc95">"keyword"</SPAN><SPAN style="color: #e6e6e6">:&#160;</SPAN><SPAN style="color: #19f9d8">"dfg15&#160;kwclickhogar18&#160;kwclickhogar19&#160;kwsemflex619&#160;kwdkids2019&#160;kwcolchonescyber"</SPAN><SPAN style="color: #e6e6e6">,</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;</SPAN><SPAN style="color: #ffcc95">"uniqueID"</SPAN><SPAN style="color: #e6e6e6">:&#160;</SPAN><SPAN style="color: #19f9d8">"241084"</SPAN><SPAN style="color: #e6e6e6">,</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;</SPAN><SPAN style="color: #ffcc95">"parentCategoryID"</SPAN><SPAN style="color: #e6e6e6">:&#160;</SPAN><SPAN style="color: #19f9d8">"10108"</SPAN><SPAN style="color: #e6e6e6">,</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;</SPAN><SPAN style="color: #ffcc95">"fullImage"</SPAN><SPAN style="color: #e6e6e6">:&#160;</SPAN><SPAN style="color: #19f9d8">"/wcsstore/ABCDIN/images/colchones-1-5-plaza/1121267F13.jpg"</SPAN><SPAN style="color: #e6e6e6">,</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;</SPAN><SPAN style="color: #ffcc95">"productType"</SPAN><SPAN style="color: #e6e6e6">:&#160;</SPAN><SPAN style="color: #19f9d8">"ItemBean"</SPAN><SPAN style="color: #e6e6e6">,</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;</SPAN><SPAN style="color: #ffcc95">"resourceId"</SPAN><SPAN style="color: #e6e6e6">:&#160;</SPAN><SPAN style="color: #19f9d8">"https://abc-live.prod.coc.ibmcloud.com/wcs/resources/lbs/store/10001/productview/byId/241084"</SPAN><SPAN style="color: #e6e6e6">,</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;</SPAN><SPAN style="color: #ffcc95">"thumbnail"</SPAN><SPAN style="color: #e6e6e6">:&#160;</SPAN><SPAN style="color: #19f9d8">"/wcsstore/ABCDIN/images/colchones-1-5-plaza/1121267F12.jpg"</SPAN><SPAN style="color: #e6e6e6">,</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;</SPAN><SPAN style="color: #ffcc95">"shortDescription"</SPAN><SPAN style="color: #e6e6e6">:&#160;</SPAN><SPAN style="color: #19f9d8">"Colch</SPAN><SPAN style="color: #45a9f9">\u00f3</SPAN><SPAN style="color: #19f9d8">n&#160;1,5&#160;Plazas&#160;Flex&#160;Adapta&#160;6"</SPAN><SPAN style="color: #e6e6e6">,</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;</SPAN><SPAN style="color: #ffcc95">"name"</SPAN><SPAN style="color: #e6e6e6">:&#160;</SPAN><SPAN style="color: #19f9d8">"Colch</SPAN><SPAN style="color: #45a9f9">\u00f3</SPAN><SPAN style="color: #19f9d8">n&#160;1,5&#160;Plazas&#160;Flex&#160;Adapta&#160;6"</SPAN><SPAN style="color: #e6e6e6">,</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;</SPAN><SPAN style="color: #ffcc95">"Price"</SPAN><SPAN style="color: #e6e6e6">:&#160;[</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;{</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;</SPAN><SPAN style="color: #ffcc95">"priceUsage"</SPAN><SPAN style="color: #e6e6e6">:&#160;</SPAN><SPAN style="color: #19f9d8">"Offer"</SPAN><SPAN style="color: #e6e6e6">,</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;</SPAN><SPAN style="color: #ffcc95">"priceDescription"</SPAN><SPAN style="color: #e6e6e6">:&#160;</SPAN><SPAN style="color: #19f9d8">"I"</SPAN><SPAN style="color: #e6e6e6">,</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;</SPAN><SPAN style="color: #ffcc95">"priceValue"</SPAN><SPAN style="color: #e6e6e6">:&#160;</SPAN><SPAN style="color: #19f9d8">"159990.0"</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;}</SPAN></DIV><DIV><SPAN style="color: #e6e6e6">&#160;&#160;&#160;&#160;&#160;&#160;],...</SPAN></DIV></DIV>
---
>**Sequence Diagram & Solution Alternatives**
::: mermaid
sequenceDiagram
    
    participant T as Totem
    participant K as kiosko AWS
    participant E as ecom
    participant C as IBM repository
    T->>K: open web
    K->>E: get rest productview
    E-->>K:response
    K-->>T:response
    loop for each image | *.jpg
      T->>C: get url img
      C-->>T:response
    end
    opt get from kiosko aws
      T->>K: get url img
      K-->>T:response
    end
    opt get from local
      T->>T: get local img
    end
:::
