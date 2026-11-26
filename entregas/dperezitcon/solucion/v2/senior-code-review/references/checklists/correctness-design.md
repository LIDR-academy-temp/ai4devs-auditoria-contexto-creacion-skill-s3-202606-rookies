# Checklist — Corrección, diseño, pruebas y código generado con IA

Aplica solo lo pertinente y registra lo no evaluado.

## Arquitectura y diseño
- Límites de módulos y contextos de dominio; cohesión, acoplamiento, dependencias y ciclos.
- Separación entre dominio, aplicación, infraestructura y presentación cuando sea apropiado; reglas de dependencia, abstracciones justificadas, contratos y responsabilidad de componentes.
- SOLID, DRY, KISS y YAGNI de forma pragmática: sobreingeniería, complejidad accidental, duplicación de reglas, abstracciones prematuras.
- Escalabilidad, coste operativo, mantenibilidad, testabilidad y evolución. No propongas microservicios, DDD o Clean Architecture sin necesidad demostrable.

## Corrección funcional y calidad
- Requisitos, criterios de aceptación, reglas de negocio, invariantes, estados y transiciones.
- Nulos, vacíos, valores extremos, errores, límites de paginación, precisión decimal, moneda, fechas y zona horaria cuando aplique.
- Tipos, excepciones, resultados silenciosos, recursos no liberados, código muerto, TODO relevantes y errores ignorados.
- Contratos de API, compatibilidad, versionado y manejo de fallos de servicios externos.

## Testing y regresión
- Pruebas unitarias de lógica, de integración de persistencia y servicios, de contrato, E2E de procesos críticos y negativas.
- Casos límite, roles, permisos, concurrencia, idempotencia, fallos parciales, migraciones y regresiones.
- Determinismo, aislamiento, aserciones sobre efectos reales, fixtures y mocks proporcionados.

## Código generado con IA (y sistemas que integran IA)
- APIs o bibliotecas inventadas, implementaciones aparentes, funciones sin uso, wrappers redundantes y patrones incompatibles con el repositorio.
- Pruebas que validan la implementación en vez del comportamiento requerido; simulaciones que encubren defectos.
- Si el producto usa LLM: entradas no confiables, prompt injection, autorización de herramientas, minimización de datos, validación de salidas, límites de coste y supervisión humana para acciones sensibles.
- Evalúa el código por sus efectos, independientemente de que su autor sea humano o IA.
