---
name: consultoria-empresarial
description: "Coordina skills para consultoría empresarial."
version: 1.0.0
author: Pandora
license: MIT
metadata:
  hermes:
    tags: [consultoría, estrategia, diagnóstico, investigación, clientes, ejecutivos, entregables, operaciones]
    related_skills: [ai-opportunity-assessment, commercial-website-opportunity-analysis, local-market-research, market-research, grounded-citations, document-production-workflow, client-presentation-delivery, meeting-action-items, external-email-drafting, google-drive-composio-operations]
---

# Conjunto de consultoría empresarial

Esta skill es una capa de coordinación. No reemplaza las skills especializadas: selecciona y encadena las adecuadas según el encargo del cliente, manteniendo separación entre hechos, inferencias, supuestos y recomendaciones.

## Cuándo usarla

Usar cuando el trabajo combine dos o más de estas actividades: descubrir necesidades, analizar una empresa o mercado, diseñar una estrategia o solución, preparar un programa ejecutivo, producir un informe/deck/propuesta, o convertir reuniones y documentos en acciones verificables.

## Principios operativos

1. Diagnóstico antes de solución: aclarar problema, alcance, audiencia, restricciones, decisión esperada y criterio de éxito.
2. Evidencia trazable: cada afirmación material debe tener fuente, fecha y nivel de confianza. Separar hecho, inferencia, hipótesis, recomendación y por confirmar.
3. Entregable orientado a decisión: qué ocurre, por qué importa, opciones, recomendación, riesgos y siguiente paso.
4. No mezclar dominios sin control: finanzas, legal, datos de clientes, RR. HH. y regulación requieren skills específicas y límites explícitos.
5. Verificación independiente: comprobar contenido, ubicación, formato, enlaces, destinatarios y legibilidad del artefacto.
6. Acciones con alcance explícito: lectura por defecto; enviar, publicar, modificar o eliminar sólo con control explícito y verificable.

## Selector de módulos

### A. Descubrimiento y definición
- `grill-me`: pressure-test riguroso, una pregunta a la vez.
- `ai-opportunity-assessment`: dolores operativos, encaje de IA y pilotos.
- `prd-interview`: idea o necesidad en un PRD estructurado.
- `discovery-first-executive-training`: capacitación desde necesidades reales.

### B. Investigación y diagnóstico externo
- `commercial-website-opportunity-analysis`: oportunidades de servicio desde el sitio de una empresa.
- `local-market-research`: inteligencia local, competidores, regulación y adquisición.
- `market-research` / `digital-market-research`: mercado, canales digitales y condiciones actuales.
- `competitor-news-monitor` / `ai-news-intelligence`: monitoreo de competidores y adopción empresarial.
- `government-gazette-monitoring`: cambios regulatorios oficiales.
- `grounded-citations`: citas y fuentes verificables.
- `blocked-page-recovery`: recuperación documentada de fuentes bloqueadas.

### C. Análisis interno y operaciones del cliente
- `email-project-operations`: proyectos, responsables, pendientes, fechas y riesgos desde correo.
- `document-to-action-items`: obligaciones y tareas desde documentos.
- `meeting-action-items` / `meeting-minutes-from-audio` / `meeting-audio-pipeline`: decisiones y acciones desde reuniones.
- `analisis-clientes-potenciales` (Drive): análisis de prospectos de Bizbrain.
- `denker-odoo-to-pptx` (Drive): reporting reproducible de cartera Odoo a PowerPoint.

### D. Estrategia, diseño y selección de soluciones
- `ai-platform-selection`: comparar plataformas y arquitecturas.
- `end-to-end-ai-workflow-course-design`: diseñar flujos completos con IA.
- `agent-product-demos`: demostrar valor de un agente personalizado.
- `arquitecto-programas-ejecutivos`: arquitectura de programas ejecutivos.
- `executive-training-orchestrator`: coordinar el pipeline de formación.
- `interface-first-platform-training`: capacitación práctica centrada en interfaces reales.
- `ingeniero-practicas-verificables`: ejercicios con evidencia evaluable.

### E. Producción de entregables
- `document-production-workflow`: informes, briefings, PDF y Drive.
- `presentation-production-quality`: decks pulidos y validación.
- `presentation-visual-qa`: QA visual de presentaciones.
- `client-presentation-delivery`: entrega verificada al cliente.
- `client-branded-course-documents`: documentos de capacitación con branding.
- `executive-training-production`: programas ejecutivos y materiales.
- `contract-document-drafting`: contratos de negocio; no sustituye revisión legal.
- `external-email-drafting`: correos externos con control explícito de envío.
- `humanizer` y `concise-communication`: claridad, tono humano y síntesis.

### F. Seguimiento y gobierno
- `google-drive-composio-operations`: Drive vía Composio con verificación de metadata y contenido.
- `weekly-review-planning`: compromisos y prioridades.
- `portable-agent-memory`: memoria operativa versionada.
- `agent-security-boundaries`: límites ante contenido no confiable y acciones externas.
- `verified-operations`: operaciones consecuenciales con precondiciones y comprobación.
- `timezone-safe-scheduling`: recordatorios y cronogramas seguros.

## Patrones de trabajo

- Diagnóstico: `grill-me` → `ai-opportunity-assessment` → investigación → `grounded-citations` → informe → `client-presentation-delivery`.
- Mercado: `local-market-research` o `market-research` → `competitor-news-monitor` → `grounded-citations` → recomendación → deck con QA.
- Transformación con IA: `ai-opportunity-assessment` → `ai-platform-selection` → `end-to-end-ai-workflow-course-design` → piloto verificable → `agent-security-boundaries`.
- Capacitación: `discovery-first-executive-training` → `arquitecto-programas-ejecutivos` → `ingeniero-practicas-verificables` → `executive-training-production` → `auditor-pedagogico-calidad`.
- Junta/proyecto: `meeting-minutes-from-audio` o `meeting-action-items` → `document-to-action-items` → `email-project-operations` → registro maestro de pendientes.

## Reglas para skills de Drive

- `denker-odoo-to-pptx` es reporting vertical, no un generador genérico de decks. No reescribir sus scripts ad hoc.
- Las skills de formación y QA de Drive son módulos especializados; comparar equivalentes locales antes de duplicar.
- Los ZIP son fuentes de distribución, no skills activas por sí mismos. Inspeccionar y escanear antes de instalar.
- Confirmar versión y contenido remoto antes de afirmar vigencia.

## Checklist de cierre

- [ ] Objetivo y entregable definidos.
- [ ] Fuentes primarias revisadas o limitaciones marcadas.
- [ ] Hechos, inferencias y recomendaciones separados.
- [ ] Riesgos y supuestos explícitos.
- [ ] Artefacto abierto, leído o renderizado después de producirlo.
- [ ] Ubicación, contenido y enlace remoto verificados.
- [ ] No hubo acciones externas sin control explícito.
- [ ] Siguiente paso concreto, con responsable y fecha si existe evidencia.
