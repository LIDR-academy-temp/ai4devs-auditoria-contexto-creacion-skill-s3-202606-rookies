# Severidad, confianza y quality gate

## Severidad
| Nivel | Criterio orientativo | Acción |
|---|---|---|
| P0 Crítico | Explotación grave plausible, compromiso sistémico, pérdida masiva de datos, caída crítica sin alternativa. | Bloquear integración/despliegue. |
| P1 Alto | Fallo funcional importante, bypass de autorización, corrupción de datos, regresión grave o riesgo operativo significativo. | Corregir antes de integrar/desplegar. |
| P2 Medio | Defecto real de impacto limitado, degradación relevante o deuda con riesgo concreto. | Planificar; bloquear si afecta a un requisito obligatorio o proceso crítico. |
| P3 Bajo | Problema menor de mantenibilidad o calidad con impacto acotado. | Corregir cuando sea razonable. |
| Sugerencia | Alternativa de diseño o estilo sin defecto material demostrado. | Opcional; no bloquea por sí sola. |

Valora alcance, probabilidad, explotabilidad, frecuencia, reversibilidad, criticidad y controles compensatorios reales.

## Confianza
- Alta / Media / Baja, **registrada aparte** de la severidad.
- Un riesgo potencialmente grave pero no confirmado requiere validación urgente, no afirmaciones categóricas.
- No asignes CVSS sin datos suficientes. No uses puntuaciones agregadas para ocultar bloqueantes.

## Quality gate
- **GO:** sin bloqueantes confirmados dentro del alcance; verificaciones esenciales suficientes; sin riesgos residuales incompatibles con la entrega.
- **GO condicionado:** sin P0/P1 confirmados ni incumplimientos obligatorios; riesgos o pendientes acotados, con condiciones explícitas antes de la acción pertinente y aceptación por el responsable.
- **NO-GO:** P0/P1 confirmado, incumplimiento de un requisito crítico, regresión grave o riesgo residual inaceptable. No permite el merge o release evaluado.
- **NO EVALUABLE:** faltan accesos, contexto o verificaciones esenciales para una decisión fundada. Si ya existe un bloqueante confirmado, emite NO-GO aunque falten otras verificaciones.

Si faltan verificaciones esenciales, no apruebes sin condiciones. El veredicto es una recomendación técnica, no una autorización de despliegue ni una certificación de seguridad. El responsable humano conserva la decisión.
