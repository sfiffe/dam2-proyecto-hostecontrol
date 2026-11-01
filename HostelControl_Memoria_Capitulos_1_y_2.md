# HostelControl (HCONTROL): Memoria Técnica, Capítulos 1 y 2

> Documento en construcción. Cada apartado se incorpora mediante su propia issue y PR.

## Capítulo 2: Antecedentes y Estado del Arte

### 2.1. Revisión de Sistemas Existentes

Se han analizado cuatro alternativas: dos soluciones comerciales (una de ellas de referencia en España), un proyecto de código abierto y el método manual más extendido en el sector. El análisis es documental: se basa en la información pública de los fabricantes y en directorios de software (Capterra, Software DOIT), que se indican como fuentes secundarias. En el caso de Gstock se ha consultado además su web oficial. En esta versión no se han probado las demos ni el periodo de prueba, por lo que las valoraciones se limitan a lo que las fuentes documentan y a su comparación con el alcance de HostelControl.

#### 2.1.1. Gstock

- **Tipo:** Comercial, SaaS (suscripción)
- **Plataforma:** Web, con aplicaciones móviles iOS y Android
- **URL oficial:** https://g-stock.es [12]
- **Fuente secundaria:** https://www.capterra.es/software/1019904/gstock [13]

Gstock es una plataforma de gestión de compras, escandallos, stock y consumos para restaurantes, hoteles, dark kitchens, catering y cadenas [12]. Según su web, el coste de los escandallos se recalcula al actualizarse los precios de compra, emite alarmas por variación de precios y de coste de recetas, se integra con TPV y ERP [12], [14] y ofrece como módulo adicional la digitalización de albaranes por OCR [12]. Se comercializa en cuatro planes (Zero, One, Premium y Premium + Ventas) y la web no publica precios, sino que remite a solicitar tarifas [12]. Como referencia, Capterra indica planes desde 43,90 €/mes en su listado español y desde 56 € por funcionalidad y mes en el internacional [13], [15]; las cifras difieren, por lo que deben tomarse como orientativas. Su enfoque es el control de stock y el coste real frente al teórico; las fuentes consultadas no documentan un presupuesto mensual preventivo ni un colchón financiero.

**Por qué no se toma como referencia principal:** cubre muy bien el inventario y el escandallo, pero su precio no es público, está orientada también a cadenas y grupos, y no resuelve la conexión entre compras, presupuesto y colchón financiero, que es el núcleo de HostelControl.

#### 2.1.2. Apicbase

- **Tipo:** Comercial, SaaS (suscripción)
- **Plataforma:** Web / nube, con acceso móvil
- **URL oficial:** https://www.apicbase.com [16]
- **Fuente secundaria:** https://www.capterra.com/p/171584/Apicbase-Restaurant-Management/pricing/ [17]

Apicbase ofrece gestión de recetas, planificación de menús, inventario, órdenes de compra y seguimiento de costes, con informes, soporte multilocal e integraciones con TPV y contabilidad [17]. Se factura «por funcionalidad y mes», con un plan Basic desde 249 € mensuales según Capterra [17]. Destaca por su enfoque en recetas y en operaciones de varios establecimientos, y atiende tanto a negocios pequeños como a grupos, hoteles y catering.

**Por qué no se toma como referencia principal:** su amplitud de módulos y su precio de entrada resultan, a juicio del equipo, sobredimensionados para un bar independiente, y la fuente consultada no recoge una función de colchón financiero preventivo.

#### 2.1.3. Grocy (código abierto)

- **Tipo:** Open source (licencia MIT)
- **Plataforma:** Aplicación web autoalojada (PHP)
- **Repositorio oficial:** https://github.com/grocy/grocy [18]

Grocy se define como un sistema de gestión de alimentos y hogar autoalojado, con gestión de existencias, lista de la compra y recetas, y se distribuye bajo licencia MIT [18]. Su fortaleza es el coste nulo de licencia y la posibilidad de ejecutarlo en infraestructura propia, incluso mediante contenedores Docker.

**Por qué no se toma como referencia principal:** es un sistema doméstico, no hostelero, por lo que carece de roles de gerente y encargado, presupuesto mensual, proyecciones o alertas de desviación, y su operación exige que el propio local instale y mantenga el servidor.

Como alternativa de código abierto más cercana a la hostelería se localizó **Roux**, un proyecto que combina recetas, costes de ingredientes e inventario para restauración [19]. Se descartó como referencia principal porque es un repositorio personal muy poco difundido (una sola estrella en GitHub en la fecha de consulta) y con licencia AGPL-3.0, lo que ofrece pocas garantías de continuidad y soporte.

#### 2.1.4. Método manual: hojas de cálculo y memoria

- **Tipo:** Método manual / herramienta genérica
- **Plataforma:** Escritorio (hoja de cálculo) o papel

Es la práctica predominante en un sector donde solo el 15,9 % de los establecimientos está altamente digitalizado [3]. Una hoja de cálculo es flexible y barata, pero depende de la disciplina del usuario: no impone validación de importes ni control de versiones, no ofrece transacciones ni acceso concurrente seguro desde varios dispositivos, y no recalcula los escandallos cuando cambia un precio salvo que se mantengan las fórmulas manualmente. Es, por tanto, insuficiente cuando varias personas registran compras y el margen es estrecho.

### 2.2. Análisis Comparativo (Benchmarking)

La tabla compara únicamente criterios que pueden respaldarse con las fuentes citadas o que derivan del diseño de HostelControl. Los criterios de rendimiento, accesibilidad y persistencia transaccional no se comparan con terceros, porque sus fabricantes no publican datos contrastables; para HostelControl se plantean como objetivos medibles propios (OE-01, OE-02 y OE-03) que se verificarán en el Capítulo 5.

| Criterio | Gstock | Apicbase | Grocy | Hoja de cálculo | HostelControl |
|---|---|---|---|---|---|
| Modelo y coste | Suscripción por planes; precio bajo consulta en la web oficial [12]; Capterra indica desde 43,90 a 56 €/mes [13], [15] | Suscripción; plan Basic desde 249 €/mes por funcionalidad [17] | Gratuito (licencia MIT) [18] | Licencia ofimática o gratuita | Sin licencia de software; coste de la infraestructura cloud |
| Plataforma | Web y apps iOS/Android [12] | Web y móvil [17] | Web autoalojada (PHP) [18] | Escritorio | Escritorio WPF, Android y API REST |
| Recetas y escandallos | Sí, escandallos dinámicos que se recalculan al cambiar precios [12] | Sí, con cálculo de coste de alimentos [17] | Recetas y existencias domésticas [18] | Manual, con fórmulas propias | Sí (CU-03), con recálculo automático (CU-05) |
| Alertas | Alarmas por variación de precios y costes [12] | No figura entre sus funciones [17] | No | No | Alertas por desviación presupuestaria (CU-05) |
| Integración con TPV | Sí, con TPV y ERP [12], [14] | Sí, con TPV y contabilidad [17] | No es su ámbito | Importación manual | No (fuera de alcance) |
| Presupuesto preventivo y colchón financiero | No figura entre sus funciones [12] | No figura entre sus funciones [17] | No | Solo si se construye a mano | Sí (CU-04), con alertas |
| Multilocal | Sí, orientado también a grupos [12] | Sí [17] | No | No aplica | No (excluido del alcance) |

La comparación muestra un patrón claro. Las soluciones comerciales cubren muy bien el inventario y el escandallo, y Gstock incluso recalcula los costes y avisa de variaciones de precio, por lo que el recálculo automático no es, por sí solo, un elemento diferencial. **El espacio que ocupa HostelControl es conectar compras y escandallos con un presupuesto mensual preventivo y un colchón financiero en un único flujo**, algo que ninguna de las fuentes públicas consultadas documenta. La solución de código abierto elimina el coste pero no está pensada para un negocio, y el método manual no ofrece garantías de integridad. En contrapartida, el sistema propuesto renuncia deliberadamente a funciones que sí ofrecen los competidores (TPV, multilocal, OCR, informes avanzados), tal como se delimitó en el apartado 1.4. Como limitación del análisis, al no haberse probado las demos ni el periodo de prueba, es posible que alguna funcionalidad no documentada exista en los productos comerciales.

## Bibliografía (referencias de este apartado)

[3] «Un 16 % de los establecimientos de hostelería tiene un alto nivel de digitalización», Software DOIT (resumen, no el informe original, del Informe de la Digitalización del Sector Horeca en España de BCC Innovation y Delectatech; año del informe no indicado en la fuente). [En línea]. Disponible en: https://www.softwaredoit.es/actualidad/un-16-de-los-establecimientos-de-hosteleria-tiene-un-alto-nivel-de-digitalizacion.html. Accedido: 1 nov. 2026.

[12] Gstock, «Gstock: plataforma integral de gestión de stocks en hostelería» y «Planes Gstock», sitio web oficial, s. f. [En línea]. Disponible en: https://g-stock.es/ y https://g-stock.es/planes-gstock/. Accedido: 1 nov. 2026.

[13] Capterra, «Gstock», ficha de producto (fuente secundaria). [En línea]. Disponible en: https://www.capterra.es/software/1019904/gstock. Accedido: 1 nov. 2026.

[14] Software DOIT, «Gstock» (fuente secundaria). [En línea]. Disponible en: https://www.softwaredoit.es/gstock/gstock.html. Accedido: 1 nov. 2026.

[15] Capterra, «Gstock Pricing 2026» (fuente secundaria). [En línea]. Disponible en: https://www.capterra.com/p/237539/Gstock/pricing/. Accedido: 1 nov. 2026.

[16] Apicbase, sitio web oficial del fabricante, s. f. [En línea]. Disponible en: https://www.apicbase.com. Accedido: 1 nov. 2026.

[17] Capterra, «Apicbase Restaurant Management», ficha y precios (fuente secundaria). [En línea]. Disponible en: https://www.capterra.com/p/171584/Apicbase-Restaurant-Management/pricing/. Accedido: 1 nov. 2026.

[18] Grocy, «grocy – ERP beyond your fridge!», repositorio oficial en GitHub, licencia MIT, s. f. [En línea]. Disponible en: https://github.com/grocy/grocy. Accedido: 1 nov. 2026.

[19] Xaque8787, «Roux: Food and Labor Cost Tracking, Inventory Management, Recipe Catalog…», repositorio en GitHub, licencia AGPL-3.0. [En línea]. Disponible en: https://github.com/Xaque8787/roux. Accedido: 1 nov. 2026.
