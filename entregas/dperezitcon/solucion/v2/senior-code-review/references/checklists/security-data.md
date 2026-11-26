# Checklist — Seguridad, privacidad, datos, concurrencia e integraciones

Aplica solo lo pertinente y registra lo no evaluado.

## Seguridad y privacidad
- Usa OWASP ASVS y CWE como referencias; cita identificadores solo si puedes verificarlos con una fuente consultable. Si no, describe la debilidad sin identificador.
- Autenticación; expiración, revocación y rotación de sesiones; autorización por recurso y acción; privilegio mínimo; aislamiento de tenants y usuarios.
- IDOR/BOLA, escalada de privilegios, inyección, XSS, CSRF, SSRF, deserialización, path traversal, subida de archivos y abuso de APIs, según la superficie.
- Validación en servidor, tratamiento de salida, consultas parametrizadas, secretos en código o configuración, cifrado, dependencias vulnerables, permisos y datos personales en logs.
- Rate limiting, controles antifraude cuando proceda, configuración segura y límites de confianza. No confíes en controles exclusivamente de interfaz.

## Datos, concurrencia e integraciones
- Integridad referencial, restricciones, unicidad, índices, nulos, migraciones, retención y borrado.
- Atomicidad, aislamiento, consistencia, límites de transacción, condiciones de carrera, TOCTOU, deadlocks y actualizaciones perdidas.
- Idempotencia, reintentos acotados, backoff, duplicación, orden de eventos, reconciliación, compensación y fallos parciales.
- Integraciones con sistemas externos (p. ej. ERP, CRM, APIs de terceros): conciliación, mapping, propiedad del dato, trazabilidad, cambios de esquema, reenvíos y recuperación. Aislamiento multiempresa cuando aplique.
