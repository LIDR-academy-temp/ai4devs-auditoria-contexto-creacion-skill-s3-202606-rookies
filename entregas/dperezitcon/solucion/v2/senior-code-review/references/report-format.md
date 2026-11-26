# Formato del informe

## Informe breve (PR pequeña)
1. Hallazgos accionables por severidad, con ubicación precisa y comentario breve.
2. Validación: comandos ejecutados y su resultado real, o "revisión estática".
3. Limitaciones y categorías no evaluadas.
4. Veredicto del quality gate y condiciones.

## Informe completo (auditoría, release o PR grande)
1. **Resumen ejecutivo:** conclusión, principal riesgo, alcance y decisión propuesta.
2. **Contexto y cobertura:** versiones/commits, módulos y flujos examinados, supuestos, exclusiones, revisión estática o dinámica.
3. **Hallazgos:** por prioridad, con la ficha siguiente. Si no hay hallazgos confirmados, dilo expresamente; eso no equivale a ausencia de defectos.
4. **Evaluación arquitectónica:** aciertos, riesgos, trade-offs y alternativas proporcionadas.
5. **Validación:** comandos, resultado real, tests que faltan, comprobaciones no realizadas y motivo.
6. **Plan de remediación:** dependencias, prioridad, corrección y criterio de aceptación. Distingue imprescindible de mejora.
7. **Quality gate:** veredicto, razones, condiciones y riesgos residuales.

## Ficha de hallazgo
- **ID y título:** `[P1] H-001 — descripción concreta del defecto`. IDs estables.
- **Estado:** confirmado / riesgo por validar / sugerencia (naturaleza del hallazgo).
- **Origen:** introducido / preexistente / no determinado.
- **Confianza:** Alta / Media / Baja (solidez de la evidencia; independiente del estado).
- **Evidencia:** commit si procede, ruta, símbolo y líneas verificadas; fragmento breve solo si aporta. Sin líneas fiables, indica símbolo y archivo.
- **Escenario:** precondiciones, flujo y resultado observado o derivado; comportamiento esperado.
- **Impacto:** seguridad, negocio, datos, rendimiento u operación; alcance y controles compensatorios.
- **Recomendación:** cambio mínimo, criterio de aceptación y prueba de regresión.
- **Referencia:** normativa o técnica solo si es relevante y comprobada.

No repitas el mismo hallazgo en varias categorías. Separa los riesgos por validar y las sugerencias de los defectos confirmados.

## Ejemplo de hallazgo (ficticio, ilustrativo)
> **[P1] H-001 — El reembolso no comprueba que el pedido pertenezca al usuario (IDOR)**
> - Estado: confirmado · Origen: introducido · Confianza: Alta
> - Evidencia: `src/orders/refund.service.ts`, `requestRefund()`, líneas 42-51: obtiene el pedido por `orderId` sin filtrar por `userId`.
> - Escenario: un usuario autenticado envía `POST /refunds` con el `orderId` de otro cliente → se crea el reembolso. Esperado: 404/403.
> - Impacto: fraude económico y acceso a datos de terceros; no hay control compensatorio en middleware.
> - Recomendación: filtrar por `orderId` **y** `userId` en la consulta. Criterio: un pedido ajeno devuelve 404. Prueba de regresión: test de integración con dos usuarios.

## Ejemplo de informe breve (ficticio, ilustrativo)
> **Modo:** PR/diff · base `main@a1b2c3d` · 3 ficheros, 58 líneas · revisión estática y tests.
> **Hallazgos**
> - [P1] H-001 — IDOR en `requestRefund()` (ver ficha).
> - [P3] H-002 — `formatAmount()` duplica la lógica de `money.ts:12`; consolidar.
> **Validación:** `npm test` → 112 superados, 0 fallidos. No ejecutado: tests E2E (sin entorno).
> **No evaluado:** rendimiento, frontend.
> **Quality gate: NO-GO** — P1 confirmado (H-001). Condición: corrección y test de regresión.
