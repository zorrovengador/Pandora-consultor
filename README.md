# Pandora-consultor

Conjunto curado de skills de Hermes Agent para consultoría empresarial.

## Alcance

Este repositorio reúne capacidades para:

- detectar necesidades y dolores operativos;
- cuestionar ideas, propuestas y decisiones;
- evaluar oportunidades de IA y seleccionar pilotos;
- investigar empresas, mercados y competencia;
- trabajar con evidencia y citas verificables;
- convertir reuniones y documentos en acciones;
- preparar diagnósticos y recomendaciones ejecutivas.

## Skills incluidas

| Skill | Uso principal |
|---|---|
| `consultor-discovery` | Discovery estructurado y pressure-test de ideas, problemas y decisiones. |
| `consultor-ai-needs` | Diagnóstico de oportunidades de IA y priorización de pilotos de 30 días. |
| `consultor-market-diagnostic` | Investigación de mercado local, competencia, regulación y GTM. |
| `consultor-evidence` | Citas, fuentes, trazabilidad y separación entre hechos e inferencias. |
| `consultor-meeting-actions` | Decisiones, responsables, fechas y acciones desde reuniones. |
| `consultor-document-actions` | Obligaciones, riesgos y tareas extraídas de documentos. |

## Skills complementarias recomendadas

Para una instalación completa de Hermes, este conjunto puede combinarse con las skills oficiales/locales `document-production-workflow`, `external-email-drafting`, `email-project-operations`, `google-drive-composio-operations`, `verified-operations` y `agent-security-boundaries`.

## Principios

1. Diagnóstico antes de solución.
2. Hechos, inferencias, hipótesis y recomendaciones separados.
3. No inventar dueños, fechas, precios, métricas ni estados.
4. Toda recomendación termina en una decisión, piloto o siguiente acción.
5. Preparar no significa enviar, publicar, modificar ni borrar.
6. Las acciones externas requieren autorización y verificación independiente.

## Instalación

Cada skill se encuentra en `skills/productivity/<nombre>/SKILL.md`. Copia la carpeta elegida al árbol de skills de Hermes o usa el instalador de skills correspondiente. Las skills son guías operativas; sus conectores, permisos y fuentes de datos deben configurarse por separado.

## Licencia

MIT.
