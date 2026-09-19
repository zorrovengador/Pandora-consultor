---
name: online-sku-price-reports
description: Busca precios de SKUs y crea reportes HTML interactivos.
version: 0.1.0
author: Manuel Hernández, Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [Prices, SKUs, Marketplaces, HTML, Research]
    related_skills: [product-price-monitor]
---

# Online SKU Price Reports Skill

Usa este skill cuando Amo pida buscar el precio actual de un SKU en marketplaces, comparar países o generar un reporte interactivo como el comparativo del BenQ GW2791. El resultado debe ser un archivo HTML autocontenido, con datos observados, enlaces a ofertas, disponibilidad y estadísticas auditables.

## When to Use

- Buscar un SKU en marketplaces de uno o varios países.
- Comparar Amazon, Mercado Libre, Walmart, marketplaces locales y retailers relevantes.
- Generar una gráfica de precio mínimo, máximo y promedio.
- Crear un reporte HTML interactivo con filtros, pestañas por país y enlaces específicos.

Don't use for:

- Alertas recurrentes de precio; usar `product-price-monitor`.
- Precios históricos que no estén publicados por una fuente consultable.
- Productos sustitutos cuando el SKU exacto no aparece; reportarlos aparte y claramente como sustitutos.

## Prerequisites

- SKU exacto y, si es ambiguo, marca/modelo o categoría.
- Países o mercados solicitados.
- Moneda local preferida para cada país.
- Usar `web_search` y `web_extract`; no iniciar sesión ni introducir credenciales.
- Para persistencia, usar la conexión Supabase activa mediante Composio; no pedir ni imprimir tokens.
- El reporte no depende de librerías externas: CSS y JavaScript deben quedar embebidos en el HTML.

## Quick Reference

1. Buscar el SKU con consultas específicas por país y marketplace.
2. Extraer páginas de producto, comparadores y retailers.
3. Registrar cada oferta: país, marketplace, vendedor, precio, moneda, disponibilidad, envío, URL y fecha.
4. Excluir variantes, accesorios y sustitutos de las estadísticas principales.
5. Calcular mínimo, máximo y promedio por país, sin mezclar divisas.
6. Crear HTML autocontenido en el perfil activo.
7. Validar el HTML, JavaScript, conteo de ofertas y enlaces.
8. Persistir la corrida y sus observaciones en Supabase cuando la conexión esté activa.

## Supabase persistence

Usar Composio para resolver y verificar el proyecto Supabase `PriceMonitor`; no asumir un `project_ref` ni ejecutar herramientas sin confirmar una conexión activa. El esquema normalizado ya creado usa:

- `public.sku_products`: catálogo y resolución del SKU.
- `public.price_runs`: una corrida batch, países, estado y reporte generado.
- `public.price_observations`: una fila por oferta observada, con moneda, envío, disponibilidad, confianza y URL.
- `public.price_summary`: vista agregada por SKU, país y moneda.

Flujo de persistencia:

1. Resolver el proyecto con `SUPABASE_LIST_ALL_PROJECTS` y seleccionar el proyecto `PriceMonitor` activo.
2. Leer tablas/esquemas con `SUPABASE_LIST_TABLES` y `SUPABASE_GET_TABLE_SCHEMAS` antes de insertar.
3. Crear una fila `price_runs` en estado `running`.
4. Hacer upsert lógico del SKU en `sku_products` y guardar cada oferta en `price_observations`.
5. Actualizar la corrida a `completed`, `partial` o `failed` con `finished_at` y la ruta del HTML.
6. Leer `price_summary` y las observaciones de la corrida para verificar la escritura exacta.

No guardar HTML completo ni credenciales en la base por defecto. Guardar sólo `report_path` y datos normalizados; si después se requiere almacenamiento remoto del HTML, tratarlo como una autorización separada.

## Procedure

### 1. Fijar el producto

- Buscar el SKU entre comillas y añadir marca/categoría si hay homónimos.
- Confirmar que el título, modelo, tamaño, variante y condición coincidan.
- Si aparecen variantes como `GW2791L`, `GW2790` o kits, excluirlas salvo que Amo las pida.
- Criterio de término: cada oferta incluida identifica explícitamente el SKU o un modelo inequívoco.

### 2. Diseñar la búsqueda por mercado

- Para cada país, consultar el dominio local de Amazon y los marketplaces o retailers principales.
- Usar consultas en el idioma local cuando mejoren la cobertura: `precio`, `Preis`, `価格`, `SKU` y el modelo.
- Hacer búsquedas paralelas independientes con `web_search`.
- Priorizar páginas de oferta directa; usar comparadores como respaldo y etiquetarlos como agregadores.
- Criterio de término: cada país tiene una lista de fuentes consultadas y los bloqueos o páginas sin precio quedan registrados.

### 3. Extraer y normalizar ofertas

Por cada oferta, registrar:

- país y moneda local;
- marketplace/retailer;
- vendedor;
- precio mostrado y, si está visible, envío, impuestos y total;
- estado: disponible, agotado, descontinuado, precio indexado o disponibilidad por confirmar;
- URL específica de la oferta;
- fecha y hora de consulta.

No inventar precios a partir de snippets incompletos. Si el precio sólo aparece en un resultado de búsqueda, marcarlo como `indexado`. Si una página muestra precio pero no permite confirmar compra, marcar disponibilidad por confirmar. Mantener el precio publicado en moneda local.

Criterio de término: cada fila tiene una fuente URL, moneda, precio, estado y una nota de incertidumbre cuando aplique.

### 4. Separar observaciones de estadísticas

- Calcular mínimo, máximo y promedio usando precios del producto en una misma moneda y país.
- No convertir monedas salvo que Amo lo pida explícitamente y se obtenga una tasa fechada.
- Por defecto, excluir sustitutos y ofertas sin precio.
- Incluir ofertas agotadas o indexadas en una sección de observaciones, pero advertir si entran en las estadísticas.
- Declarar si el promedio incluye ofertas no disponibles; preferir estadísticas de ofertas con precio visible y separar el conteo de disponibilidad.

Criterio de término: los valores del reporte se reproducen exactamente a partir de las filas incluidas.

### 5. Crear el reporte HTML

Generar un HTML autocontenido mediante `write_file`, con:

- encabezado del SKU y fecha de corte;
- pestañas o filtros por país/mercado;
- tarjetas de mínimo, promedio y máximo;
- gráfica interactiva de barras con tooltip o `title` accesible;
- detalle de cada oferta con marketplace, vendedor, precio, estado y enlace específico;
- nota visible sobre envío, impuestos, disponibilidad y límites de la búsqueda;
- diseño responsive inspirado en Stripe: fondo claro, tarjetas limpias, tipografía sans-serif, acentos azul-violeta y estados semánticos.

No incluir enlaces genéricos cuando exista una URL de producto u oferta. Para comparadores, enlazar al registro concreto o a la página del producto y etiquetar la fuente.

Criterio de término: el archivo abre sin assets remotos obligatorios y contiene todos los datos que sustentan la gráfica.

### 6. Verificar el artefacto

- Extraer el JavaScript embebido y validarlo con `node --check` mediante `terminal` si Node está disponible.
- Confirmar que no haya `<script src>` ni `<link href>` externos.
- Contar países, ofertas, barras, estadísticas y enlaces de oferta con un script de Python.
- Comprobar que mínimo, promedio y máximo del HTML coincidan con los cálculos programáticos.
- Si el navegador no puede abrir `file://`, servir temporalmente el directorio con un servidor local sólo para QA; no reportar que el navegador se validó si el acceso está bloqueado.
- Si se usó Supabase, leer de vuelta `price_runs`, `price_observations` y `price_summary`; confirmar que el conteo insertado coincide con el conteo recolectado y que el estado final no es `running`.

Criterio de término: la validación devuelve éxito, el archivo queda en una ruta absoluta del perfil activo y, cuando aplica, la corrida queda verificada en Supabase.

## Complete marketplace batch workflow

Use this procedure for the full run from workbook/list input to Supabase and the final HTML. Do not stop after search snippets or after writing a draft report.

1. **Load the SKU input.** Read XLSX/CSV/text with the spreadsheet/document tools, preserve SKU spelling exactly, deduplicate without changing identifiers, and record the requested count. Completion: every input SKU is accounted for as processed, no-result, ambiguous, or errored.
2. **Declare market scope.** For international monitor runs, use the requested countries and consult the principal marketplaces/retailers for each one. Default scope when the user asks for the prior international comparison: US `amazon.com`, `walmart.com`, `bestbuy.com`, `bhphotovideo.com`, `ebay.com`, `newegg.com`; DE `amazon.de`, `mediamarkt.de`, `saturn.de`, `otto.de`, `notebooksbilliger.de`, `alternate.de`, `cyberport.de`, `idealo.de`; JP `amazon.co.jp`, `rakuten.co.jp`, `shopping.yahoo.co.jp`, `kakaku.com`, `yodobashi.com`, `biccamera.com`. “All marketplaces” means all principal sources in the declared scope, never an unsupported claim of every marketplace on the internet. Completion: the report lists consulted sources and unresponsive sources by country.
3. **Search by SKU and source.** Run exact-SKU queries per country and marketplace with `web_search`; keep only pages whose title/model identifies the requested SKU. Exclude accessories, variants, used/reconditioned offers, recommendations, and substitutes from the main SKU statistics unless explicitly labeled. Completion: each retained row has country, marketplace, SKU, URL, price, currency, and collection timestamp.
4. **Verify direct pages.** Prefer the product/offer URL over an aggregator or search result. Use `web_extract` or browser page inspection to confirm a visible price, seller/condition, and availability. Set `source_type=direct` only when the direct page exposes the price; use `source_type=search_result` or `aggregator` otherwise. Never upgrade confidence merely because a URL looks like a product page. Completion: direct and indexed rows are distinguishable and every blocked/failed page is logged.
5. **Persist the run incrementally.** Resolve the dedicated Supabase project through Composio, create `price_runs` as `running`, upsert all requested SKUs into `sku_products`, then insert observations in country batches. Before each batch, validate the column order and allowed enum/check-constraint values. After each write, read back affected row counts. Completion: persisted row count equals the number of rows intentionally written; no SKU/country columns are swapped.
6. **Compute local and USD views.** Keep the original local price and currency immutable. For a USD view, convert directly from the source currency using a dated rate table: `USD→USD = 1`, `EUR→USD = 1 / (EUR per USD)`, `JPY→USD = 1 / (JPY per USD)`. Record the rate source and date in the report. Never route EUR or JPY through MXN unless explicitly requested. Completion: local and USD values reproduce from the stored price plus the dated FX rate.
7. **Generate the final HTML.** Create an autocontained responsive HTML with no external scripts or styles. It must include: KPI cards; filters for country, marketplace, currency, and SKU search; a local/USD toggle; direct source links; indexed/direct status; and interactive charts for minimum, average, and maximum price grouped by country and marketplace. Charts must use the same USD conversion logic as the table and show exact values on hover/focus. Completion: every displayed row comes from the collected dataset and every chart can be recomputed from it.
8. **Close and verify.** Set `price_runs` to `completed` only when all requested markets and writes passed; otherwise use `partial` and state the exact missing count. Save `report_path`, then read back `price_runs`, `price_observations`, and `price_summary`. Validate the HTML with `node --check` for embedded JavaScript and count rows, URLs, countries, marketplaces, and chart groups programmatically. Completion: report count, persisted count, and verification output agree; any disagreement is disclosed rather than silently repaired.

## Pitfalls

- Amazon y marketplaces pueden mostrar precios condicionados por código postal, sesión, membresía o ubicación.
- Un resultado de búsqueda puede estar desactualizado; marcarlo como indexado y no como oferta disponible.
- No mezclar precio base con precio total ni comparar una oferta nueva con una reacondicionada.
- No usar el precio de un accesorio, variante o producto recomendado por la página.
- Los comparadores pueden duplicar al mismo vendedor en varios marketplaces; conservar la oferta por marketplace, pero explicar duplicados cuando afecten el promedio.
- En Japón y Alemania, los agregadores pueden mostrar precios en tiendas de otros países; verificar el país de envío antes de llamarlo oferta local.
- No afirmar cobertura exhaustiva de “todos los marketplaces”; decir cuáles se consultaron y cuáles no pudieron verificarse.
- No afirmar disponibilidad cuando la fuente dice `out of stock`, `discontinued`, `no featured offer` o equivalente.

## Verification

- [ ] SKU y variante están confirmados.
- [ ] Cada país tiene fuentes consultadas y limitaciones declaradas.
- [ ] Cada oferta tiene precio, moneda, marketplace, vendedor, estado y URL.
- [ ] Sustitutos y variantes fueron excluidos de las estadísticas.
- [ ] Mínimo, máximo y promedio coinciden con los datos incluidos.
- [ ] Los precios no mezclan monedas.
- [ ] El HTML es autocontenido y responsive.
- [ ] Cada oferta tiene enlace específico o se explica por qué sólo se pudo enlazar la fuente agregadora.
- [ ] JavaScript y conteos del reporte fueron validados antes de entregarlo.