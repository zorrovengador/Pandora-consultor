---
name: consultor-evidence
description: Mantiene trazabilidad entre afirmaciones, fuentes y recomendaciones consultivas.
version: 1.0.0
author: Pandora
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [consultoría, evidencia, citas, fuentes, informes, rigor]
---

# Consultor Evidence

Usa esta skill cuando un diagnóstico, informe, comparación o recomendación dependa de información externa o de documentos del cliente.

## Procedimiento

1. Abre un ledger por tarea.
2. Registra cada URL o documento al recuperarlo, no al final desde memoria.
3. Clasifica cada afirmación como `hecho verificado`, `claim de fuente`, `inferencia`, `hipótesis` o `por confirmar`.
4. Cita inmediatamente mientras redactas.
5. Para afirmaciones críticas, conserva una cita textual o referencia exacta a página/sección.
6. Separa evidencia de recomendación y muestra qué dato podría falsar la conclusión.
7. Verifica que cada cita exista, que las fuentes listadas sean las citadas y que no haya afirmaciones materiales sin procedencia.

## Formato mínimo

Cada hallazgo debe contener: afirmación, tipo de evidencia, fuente, fecha, confianza, implicación y validación pendiente.

## Límites

Una fuente primaria demuestra lo que dice, no necesariamente que su claim sea verdadero. No inventes URLs, citas, cifras ni fechas. No uses fragmentos de buscador como prueba suficiente cuando el documento completo es accesible.

## Verificación

- [ ] No hay citas inventadas.
- [ ] Los enlaces son canónicos y accesibles.
- [ ] Se distinguen hechos, claims e inferencias.
- [ ] Las fuentes no utilizadas fueron excluidas del bloque final.
