# Evidencia — Parte A (prueba real de exploración)

- **Comando** (en una copia desechable del repositorio, remoto eliminado, fuera de OneDrive):
  `claude.exe -p "<prompt>" --model claude-sonnet-5-5 --effort medium --permission-mode dontAsk --setting-sources project --disallowedTools Edit Write NotebookEdit WebFetch WebSearch --allowedTools Read Grep Glob "Bash(git ls-files *)" "Bash(git log *)" "Bash(git status *)" --no-session-persistence --output-format text`
- **Fecha:** 2026-11-26, 16:10:41 a 16:11:07 (26 s) · **Entorno:** Windows 11, Claude Code 2.1.160 · **Salida de error:** vacía · **Código de salida:** 0.
- **Repositorio auditado:** repositorio de entrega del módulo 2 (rama `entrega-modulo-02-DPR`, commit `e8a8768`). Tras la ejecución, `git status` no mostró cambios.
- **Prompt (el del enunciado):**

```text
Explora este repositorio y dime qué entiendes de su arquitectura: stack, estructura de carpetas, cómo se arranca, convenciones que detectes. No modifiques nada, solo análisis.
```

## Respuesta literal del agente

> ## Resumen
>
> Es un repositorio de **entrega académica** (curso AI4Devs, módulo 2/3), no una aplicación. Tiene dos partes independientes que ilustran los "3 Pilares" (Herramienta, Contexto, Prompt) y el desarrollo guiado por especificaciones (Spec-Driven Development).
>
> ## Estructura
>
> ```
> .
> ├── README.md / ENTREGA.md        # Enunciado del ejercicio OpenSpec y entregable
> ├── Parte B — ... .png            # Captura de la instalación de OpenSpec
> ├── Parte A/                      # Solución .NET
> │   ├── AGENTS.md                 # Contexto/reglas para el copiloto
> │   ├── PalindromeChecker.sln
> │   ├── PalindromeChecker.Lib/    # Biblioteca de clases (StringHelper.cs)
> │   ├── PalindromeChecker.Tests/  # Proyecto xUnit
> │   └── ENTREGA.md
> └── openspec-sandbox/             # Salida de `openspec init`
>     ├── openspec/config.yaml      # schema: spec-driven, sin personalizar
>     └── .claude/{commands/opsx, skills/openspec-*}
> ```
>
> ## Stack
>
> - **Parte A:** C# sobre .NET 9 (`net9.0`), con `Nullable` e `ImplicitUsings` activados. Las pruebas usan xUnit 2.9.2, `Microsoft.NET.Test.Sdk` y `coverlet.collector`.
> - **Parte B:** OpenSpec (`@fission-ai/openspec`, requiere Node ≥ 20.19) integrado con Claude Code mediante skills y slash commands `/opsx:*` (propose, apply, archive, explore, sync, update).
>
> ## Cómo se arranca
>
> No hay punto de entrada (`Program.cs`) ni ejecutable: `Lib` es una biblioteca y solo se ejercita con tests. No he ejecutado nada, así que esto sale de leer los `.csproj`. Lo esperable sería:
>
> ```bash
> cd "Parte A"
> dotnet test
> ```
>
> Para OpenSpec, el README indica `npm install -g @fission-ai/openspec@latest` y luego `openspec init`.
>
> ## Código
>
> `StringHelper.IsPalindrome(string?)` es una función estática pura:
> - Devuelve `false` para `null`, cadena vacía o cadena sin caracteres alfanuméricos.
> - Pasa el texto a minúsculas, lo normaliza a FormD, elimina las marcas diacríticas y conserva solo letras y dígitos.
> - Compara con dos punteros.
>
> Los tests cubren `true` y `false` con `[Theory]`, además de los casos extremos (`null`, vacío, solo puntuación, espacios alrededor).
>
> ## Convenciones detectadas
>
> - **`AGENTS.md`:**
>   - Métodos estáticos en PascalCase.
>   - Sin dependencias NuGet externas (la excepción razonable son las de test).
>   - Funciones puras en archivos aislados.
> - **Tests:** nombres `Metodo_Resultado_Condicion`, agrupados con comentarios separadores, un `Assert` por test.
> - **Documentación:** XML docs y comentarios en español.
> - **Estilo:** namespaces con bloque `{}`, no file-scoped, y `using` explícitos aunque `ImplicitUsings` esté activo.
> - **`.gitignore`:** cubre .NET (`bin/`, `obj/`), Node y secretos (`.env*`, `*.pem`, `*.key`).
> - **Git:** rama de trabajo `entrega-modulo-02-DPR`, con commits en estilo mixto (`docs:` y mensajes libres).
>
> ## Observaciones
>
> - El README habla de `openspec/` en la raíz, pero aquí está dentro de `openspec-sandbox/`.
> - `config.yaml` conserva la plantilla por defecto, sin `context` ni `rules`, así que OpenSpec no tiene aún contexto del proyecto. Podría rellenarse con lo que dice `AGENTS.md`.
> - En `openspec-sandbox/` no hay `specs/` ni `changes/` versionados, solo la configuración y las skills.
