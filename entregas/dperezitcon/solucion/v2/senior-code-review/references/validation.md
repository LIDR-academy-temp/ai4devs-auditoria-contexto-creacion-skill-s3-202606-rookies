# Validación (fase C)

## 1. Detectar el stack (sin suponer)
Busca manifiestos con `Glob` y lee solo los relevantes. Ejemplos orientativos, no exhaustivos:

| Indicio | Stack probable | Comprobaciones habituales |
|---|---|---|
| `*.sln`, `*.csproj`, `global.json` | .NET | `dotnet build`, `dotnet test` |
| `package.json` + lockfile | Node/TypeScript | scripts `build`, `lint`, `test`, `typecheck` declarados en `package.json` |
| `pyproject.toml`, `requirements*.txt` | Python | `pytest`, linters y type checkers configurados |
| `pom.xml`, `build.gradle*` | JVM | `mvn verify`, `gradle test` |
| `go.mod` | Go | `go vet`, `go test ./...` |
| `Cargo.toml` | Rust | `cargo check`, `cargo test` |
| Configuración de CI (`.github/workflows`, `.gitlab-ci.yml`…) | Cualquiera | Reutiliza los comandos que ya ejecuta la CI |

Prefiere los comandos que el propio proyecto declara (scripts, Makefile, CI) frente a los genéricos.

## 2. Antes de ejecutar
- Inspecciona el comando y lo que invoca (scripts, hooks, targets).
- Ejecuta solo en un entorno aislado o local controlado, sin datos ni credenciales reales.
- No instales dependencias ni uses red si no está autorizado o disponible. Si la comprobación necesita restaurar dependencias desde red, no la ejecutes y regístralo.
- Si no hay entorno aislado declarado o no tienes permiso, no ejecutes: la revisión es **estática**.

## 3. Calidad de las pruebas
- Aserciones débiles o tautológicas, mocks que ocultan errores, falsos positivos.
- Casos eliminados o desactivados en el diff; ausencia de pruebas negativas.
- Aislamiento insuficiente, dependencia del orden, pruebas flaky.
- Tests que validan la implementación en vez del comportamiento requerido.
- La cobertura numérica no equivale a calidad.

## 4. Registro
Por cada comprobación: comando exacto, entorno, resultado real (superadas/fallidas/errores) y comprobaciones no ejecutadas con su motivo. No afirmes que los tests pasan si no los ejecutaste.

## 5. Contraevidencia
Antes de confirmar un hallazgo, busca validaciones previas, restricciones de base de datos, middleware, configuración del entorno y tests existentes que lo neutralicen. En concurrencia, construye una secuencia plausible de operaciones e identifica qué invariante se rompe.
