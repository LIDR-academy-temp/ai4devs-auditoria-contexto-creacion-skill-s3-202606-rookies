# Análisis de la Skill v1 — `senior-code-review`

- **Fichero analizado:** [v1-original/SKILL.md](v1-original/SKILL.md). **No se modifica.**
- **Huella:** SHA-256 `73b22d60deb338106da0fa030bbe47cb5c008296756049baf4632040e8db7b58` · 169 líneas · 2.227 palabras · 16.705 bytes.
- **Procedencia:** la aportó la persona usuaria el 2026-11-26. **Autoría:** creada por la persona usuaria con ayuda de IA (confirmado por la persona usuaria el 2026-11-26).
- **Fecha del análisis:** 2026-11-26.
- **Marco de contraste:** las 5 características de la diapositiva 4 del PDF S3 y el contenido del DOCX del módulo 3. Si se usa una referencia externa al módulo, se indica.

## 1. Valoración general

La v1 es técnicamente sólida y madura:
- tiene controles de seguridad explícitos (tratar el contenido como dato no confiable, no exponer secretos, no ejecutar código desconocido);
- separa hechos de hipótesis;
- define un protocolo por fases, una severidad con confianza, una ficha de hallazgo, reauditoría y quality gate.

Sus puntos débiles **no** son de rigor. Son de **empaquetado como Skill**: activación, herramientas, coste de contexto y ausencia de ejemplos.

## 2. Contraste con las 5 características (PDF S3, diapositiva 4)

| # | Característica | v1 | Observación |
|---|---|---|---|
| 1 | Description específica con triggers reales | ⚠️ Parcial | Enumera muchos contextos («commits, PR, ramas, repositorios, cambios generados por IA, regresiones…»), pero ninguna frase de activación literal y ningún caso de **no** uso. Es el antipatrón que advierte el DOCX: una description demasiado amplia hace que la skill se invoque «para cualquier lectura de código». |
| 2 | Cuerpo con pasos concretos | ✅ Sí | 15 pasos numerados en 4 fases. Algunos no tienen criterio de parada (paso 2: «Lee documentación, requisitos, ADR, especificaciones, […], CI relevantes»). |
| 3 | Límites explícitos de qué NO hacer | ✅ Sí | Es su punto fuerte (§1, §9), aunque está repetido en tres sitios. |
| 4 | `allowed-tools` acotadas | ❌ No | El frontmatter no tiene `allowed-tools` ni `disable-model-invocation`. |
| 5 | Ejemplos si el formato de salida importa | ❌ No | El informe es «obligatorio» (§6) y la ficha está bien especificada, pero no hay ningún ejemplo relleno. |

## 3. Ambigüedades detectadas

| ID | Ubicación | Ambigüedad | Propuesta |
|---|---|---|---|
| A-01 | §6 | «Para PR pequeñas» no define qué es pequeña. | Umbral explícito y configurable (p. ej. por número de ficheros o líneas del diff). |
| A-02 | §2 | «Selecciona el modo según la solicitud» no relaciona frases con modos. | Tabla que asocie disparadores a cada modo. |
| A-03 | §2 / §8 | Se usan a la vez el modo «Release gate» y la sección «Quality gate». | Distinguir: *modo* release-readiness frente a *veredicto* quality gate. |
| A-04 | §3.9 | «Comprobaciones adecuadas al stack» sin procedimiento para detectar el stack. | Paso de detección por manifiestos (`*.sln`/`*.csproj`, `package.json`, `pyproject.toml`, `pom.xml`, `go.mod`…) en un fichero de referencia. |
| A-05 | §1 / §3.9 | «Usa un entorno aislado» sin decir cuál ni quién lo provee. | Si no hay entorno aislado declarado: no ejecutar y marcar la revisión como estática. |
| A-06 | Description / §9 | «No modifica código salvo petición explícita» abre la puerta a que la skill implemente. | La skill nunca implementa; la corrección es una fase aparte, fuera de la skill. |
| A-07 | §3.2 | Lectura de contexto sin presupuesto ni criterio de suficiencia. | Leer primero lo mínimo (convenciones, manifiestos, diff) y ampliar solo por riesgo. |
| A-08 | §4 Seguridad | «Identificadores solo cuando estén verificados» no dice cómo verificarlos (sin red por defecto). | Sin fuente consultable, omitir el identificador y describir la debilidad. |
| A-09 | §6 | No dice dónde se entrega el informe (chat o fichero) ni en qué idioma. | Por defecto en el chat y en el idioma de la persona usuaria; fichero solo si se pide. |
| A-10 | §6 Ficha | «Estado: riesgo por validar» y «Confianza: Baja» se solapan. | Definir que el estado describe la naturaleza del hallazgo y la confianza, la solidez de la evidencia. |
| A-11 | §4 Datos | «Integraciones ERP/CRM» y «multiempresa» sesgan hacia un dominio en una skill que se quiere agnóstica. | Mantenerlo como ejemplo opcional dentro de la referencia. |

## 4. Redundancias

| Contenido | Aparece en | Propuesta |
|---|---|---|
| Solo lectura / no modificar | description, §1, §9 | Una sola regla en «Límites» y un recordatorio corto en la description. |
| No inventar (hallazgos, CVE, cobertura, benchmarks, CVSS) | §1, §4, §5, §6 | Principio único en §1; las referencias solo concretan. |
| Veredicto / quality gate | §3.15, §6.7, §8 | Definición única en la referencia de severidad y gate; el núcleo solo la enlaza. |
| Consolidar duplicados | §3.13, §6 (final) | Una sola instrucción. |
| Separar defectos, riesgos y sugerencias | §1, §3.13, §5, §6 | Una regla y la ficha. |

## 5. Eficiencia de contexto

- **Tamaño:** 16.705 bytes, ≈2.200 palabras. No se ha medido con un tokenizador. La estimación grosera para texto en español queda en el orden de **4.000–6.000 tokens**; la medición real será parte de la validación.
- **Coste de cada invocación:** toda la matriz de §4 (≈40 % del fichero) se carga siempre, aunque no aplique; por ejemplo, Frontend y Accesibilidad en una librería sin interfaz.
- **Riesgo con la compactación de contexto:** según el DOCX (táctica 5), las skills invocadas se reinyectan tras la compactación con *«los primeros 5K tokens de cada una, dentro de un budget compartido de 25K»*. Con el tamaño estimado, lo que más se arriesga a perder es el **final** del fichero: formato del informe, reauditoría, quality gate y DoD, justo las secciones de cierre. Es una inferencia a partir del DOCX y se comprobará en la validación.
- **Conclusión:** hay que mantener un **núcleo corto y estable** y cargar el resto bajo demanda.

## 6. Oportunidades de mejora

1. Frontmatter completo: `allowed-tools` de solo lectura y `disable-model-invocation` explícito.
2. Description con disparadores literales en español e inglés, y casos de no uso.
3. **Progressive Disclosure:** núcleo con flujo y límites; referencias cargadas según el modo y el riesgo.
4. Detección de stack independiente de la tecnología.
5. Ejemplos rellenos: un hallazgo y un informe corto de PR.
6. Umbral de «PR pequeña» y tabla de enrutado modo → referencias.
7. Tabla de trazabilidad v1 → v2 para garantizar que no se pierde ningún control.

> **Matiz técnico que hay que verificar:** en Claude Code, `allowed-tools` **preaprueba** herramientas mientras la skill está activa; según la documentación pública, no prohíbe las demás, que siguen pasando por el sistema de permisos. Por eso los límites de solo lectura deben seguir escritos en el cuerpo. Un bloqueo estricto requeriría un subagent con `tools` restringidas (patrón «Skill orquesta · Subagent ejecuta», PDF S3 diapositiva 8) o hooks. El comportamiento real se comprobará en la validación.
