---
name: consultor-meeting-actions
description: Convierte reuniones en decisiones, responsables y acciones verificables.
version: 1.0.0
author: Pandora
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [consultoría, reuniones, decisiones, acciones, seguimiento]
---

# Consultor Meeting Actions

Usa esta skill cuando existan notas o transcript de una junta y se necesite convertirlos en seguimiento operativo.

## Procedimiento

1. Identifica título, fecha, asistentes, fuente y cobertura del transcript.
2. Separa decisiones, propuestas no decididas, compromisos, bloqueadores, riesgos y contexto.
3. Para cada acción registra resultado, dueño, fecha, dependencia, aceptación y evidencia.
4. Usa `sin resolver` cuando el dueño o plazo no sean explícitos.
5. Busca registros existentes antes de proponer tickets nuevos para evitar duplicados.
6. Prepara minuta y seguimiento para revisión; redactar no equivale a enviar.
7. Sólo después de autorización crea o actualiza tareas y lee de vuelta el resultado.

## Salida

Minuta ejecutiva, tabla de decisiones, acciones, dueños, fechas, dependencias, preguntas abiertas, riesgos y próximo checkpoint.

## Verificación

- [ ] Cada acción tiene cita, timestamp o referencia de nota.
- [ ] No se inventaron responsables ni fechas.
- [ ] Se buscaron duplicados.
- [ ] Las acciones externas requieren aprobación explícita.
