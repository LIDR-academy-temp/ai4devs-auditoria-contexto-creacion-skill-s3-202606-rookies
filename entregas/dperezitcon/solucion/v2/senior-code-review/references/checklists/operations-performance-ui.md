# Checklist — Rendimiento, frontend/accesibilidad, operación y supply chain

Aplica solo lo pertinente y registra lo no evaluado.

## Rendimiento y capacidad
- Complejidad algorítmica, N+1, índices, consultas no acotadas, paginación, round trips, memoria, tareas bloqueantes y conexiones.
- Cachés y su invalidación, timeouts, concurrencia, colas, límites de recursos y backpressure.
- Separa cuellos de botella demostrados de riesgos teóricos. No inventes benchmarks; propón una medición o prueba de carga si falta evidencia.

## Frontend y accesibilidad (si aplica)
- Estados de carga, vacío y error; doble envío; condiciones de carrera; validación; sincronización de datos; errores de red.
- Semántica, teclado, foco, contraste y comportamiento responsive. Una validación de interfaz no es un control de seguridad.

## Operación, DevOps y supply chain
- CI/CD, configuración por entorno, permisos, secretos, versiones reproducibles y lockfiles, integridad de artefactos y dependencias.
- Logs estructurados, métricas, trazas, correlación, alertas accionables y health checks; protección de la información sensible.
- Despliegue seguro, compatibilidad entre versiones, migraciones, backups, restauración verificada y rollback viable. Documenta el riesgo si una migración irreversible impide un rollback simple.
