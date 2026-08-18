---
name: consultor-document-actions
description: Extrae obligaciones, riesgos y tareas trazables de documentos empresariales.
version: 1.0.0
author: Pandora
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [consultoría, documentos, obligaciones, riesgos, plazos, tareas]
---

# Consultor Document Actions

Usa esta skill para transformar contratos, informes, políticas, propuestas o anexos en hechos estructurados y acciones propuestas.

## Procedimiento

1. Identifica versión, fecha, idioma, páginas, calidad de OCR y documento autoritativo.
2. Conserva ubicación de cada dato: archivo, página, sección o tabla.
3. Clasifica entidades, fechas, dinero, obligaciones, prohibiciones, aprobaciones, riesgos y ambigüedades.
4. Mantén la modalidad: `puede`, `debería` y `debe` no son equivalentes.
5. Comprueba fechas, totales, nombres, definiciones y referencias cruzadas.
6. Convierte obligaciones en resultado, dueño explícito, fecha explícita, dependencia, aceptación, riesgo y cita.
7. Presenta hechos, riesgos y acciones para aprobación antes de escribir en trackers o calendarios.

## Límites

La extracción no es asesoría legal, fiscal, médica ni de seguridad. La baja calidad de OCR y las contradicciones deben permanecer visibles.

## Verificación

- [ ] Cada hecho y acción tiene página/sección.
- [ ] Se conserva la incertidumbre y la modalidad del texto.
- [ ] No se crearon tareas externas sin aprobación.
- [ ] El resultado separa hechos, propuestas, supuestos y bloqueadores.
