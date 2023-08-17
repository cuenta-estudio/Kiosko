Historia de usuario:
#61512

Autor, Camilo Alaniz.

[[_TOC_]]

----

#Objetivo:
Quitar de la interfaz los filtros que no están operativos luego del cambio a magento.

#Problema:
Kiosko en su selección de filtros, da la opción de aplicar unos filtros que no están funcionando, por lo que algunos provocan error al usuario o no le muestra los productos que quiere. Se necesita mitigar estas situaciones mientras se define como se integrarán a magento.

#Solución:
Para la mitigación, se añadió una funcionalidad al código para quitar el los filtros que se han especificado "Categoría", "Card Price" y "Rango de Precios".


#QA
Luego de los cambios realizados podemos ver como se visualizan los filtos y validamos la inexistencia de los filtros Categoría, Card Price, Rango de Precios:

![para la wiky .png](/.attachments/para%20la%20wiky%20-d4e48d63-2948-4fb9-adef-cb31ed2b7784.png)