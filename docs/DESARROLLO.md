# UserManager — Bitácora pedagógica retrospectiva
Documento de consulta del alumnado. No es fuente de verdad técnica. Se amplía únicamente después de realizar y verificar un paso, mediante Build y la skill documentar, con aprobación humana. No contiene pasos futuros ni resultados simulados.

*Todavía no se han registrado pasos ejecutados.*

---

## 1. Verificación del entorno, la autenticación y la autoría antes de escribir

**Objetivo.** Confirmar que las herramientas, el repo clonado, el modelo y los permisos de OpenCode, y la identidad de Git/GitHub están listos para trabajar, y que no se usa la identidad del profesorado.

**Fundamento y finalidad pedagógica.** En 2.º de FP, antes de entregar un trabajo se comprueba que la etiqueta lleva el nombre del alumno y que el instrumento está calibrado; el equivalente aquí es verificar la «etiqueta» (autor de Git y cuenta de GitHub) y el «instrumento» (versiones y permisos). Separar quién decide (persona) de quién ejecuta (agente) evita atribuir al docente una entrega del alumnado.

**Contexto.** Sin SPEC aprobada ni código generado; `constitution.md` está en borrador y no se trata como aprobado. Rama `main`. Agente Plan para la verificación; paso a Build por decisión humana para redactar este registro. No consta ejecución de `/new` en esta sesión. Skills usadas: `opencode` (interpretar modelo y permisos) y `documentar` (esta propuesta). Artefactos consultados: `AGENTS.md`, el final de `docs/DESARROLLO.md` (solo para numeración), salida de `git config`, `gh auth status` y `opencode debug config|agents|models`.

**Prompts usados y aclaraciones.**
1. «No hay prompt. Comprobar git --version, gh --version, opencode --version, dotnet --info. Autenticarse personalmente con gh auth login; gh auth status. Ya estas dentro del repo clonado. Comprobar modelo, permisos, identidad Git y que Profesor queda fuera.»
2. «Carga la skill documentar y documenta el paso que acabamos de realizar. Presenta la propuesta y espera autorización antes de añadirla.»

Se interpretó «Profesor queda fuera» como «no usar cuenta ni identidad docente»; queda pendiente confirmación humana. «No hay prompt» se entendió como que no había instrucción adicional aparte del mensaje.

**Proceso.** Se ejecutaron únicamente comandos de lectura: versiones, estado del repo, configuración de Git, estado de `gh`, modelos/agentes/configuración de OpenCode y búsqueda de «Profesor». No se crearon archivos ni se hicieron commits. `gh auth login` no se ejecutó: es interactivo y personal, y ya existía sesión activa; su renovación queda en manos del humano. La escritura de este registro se propuso y se ha aplicado tras autorización explícita.

**Decisiones y alternativas.** Decisión humana: verificar antes de escribir y documentar después. Alternativa descartada: ejecutar `gh auth login` desde el agente (es personal y modificaría credenciales globales). Alternativa pendiente: si se quiere renovar la sesión de GitHub, el humano ejecuta `gh auth login` y `gh auth status`.

**Responsabilidad.** Ningún archivo fue modificado en el paso verificado: el agente solo leyó; el humano decide la autenticación y autorizó esta escritura. Solo se ha modificado `docs/DESARROLLO.md`, conservando intactas las líneas 1-4, incluido el marcador inicial.

**Comandos y resultados reales.** (Se omiten correo, usuario literal y token para no registrar datos personales o credenciales.)
- `git --version` → `2.55.0.windows.5`; `gh --version` → `2.101.0`; `opencode --version` → `v2.4.1`; `dotnet --info` → SDK `10.0.301`, runtime `10.0.9`, workload `maui-windows`, sin `global.json`.
- `git status --short --branch` → `## main...origin/main`, sin cambios; `git remote -v` → remoto `https://github.com/<cuenta>/Prueba_SDD.git`.
- `git config --show-origin --get user.name|user.email` → identidad del alumnado en `.gitconfig` global; `git log -5 --format='%h | %an <%ae> | %s'` → único commit `fb400c8` con esa misma identidad.
- `gh auth status` → sesión activa en github.com para la cuenta del alumnado, vía keyring, protocolo `https`, scopes `gist`, `read:org`, `repo`, `workflow`. Valor del token no registrado.
- `gh api repos/<owner>/Prueba_SDD/collaborators --jq '.[].login'` → solo la cuenta del alumnado.
- `opencode models | Select-String big-pickle` → `opencode/big-pickle`; `opencode debug config` → única fuente `~/.config/opencode`; `opencode debug agents` → agentes por defecto (`build`, `plan`, …), sin agente «Profesor»; el agente `plan` tiene `edit` denegado salvo `~/.opencode/plan/*`.
- Búsqueda de `Profesor` en la configuración de OpenCode, en el repo y en `git config` → 0 coincidencias.

**Errores y resolución.** No hubo fallos de ejecución. La ruta `~/.opencode` no existe y no se creó (no se escribió ningún plan file). La consola mostró caracteres mal codificados al consultar el final de `DESARROLLO.md` con `Get-Content`; se volvió a leer con la herramienta de lectura, sin modificar el archivo.

**Conceptos aprendidos y punto de control.** Una herramienta reproducible se verifica antes de usarla; la procedencia se comprueba en `git config`, en los commits y en la cuenta activa de `gh`, no solo en uno de esos sitios; los permisos del agente Plan limitan la escritura. Ejemplo de 2.º FP: antes de soldar se calibra el soldador, y antes de publicar se revisa la etiqueta del trabajo y el alcance del token. Punto de control: no escribir ni hacer commit sin que el humano confirme autenticación e identidad; la confirmación de «Profesor» sigue pendiente.

---

## 2. Aprobación y escritura de la constitución como base del SDD

**Objetivo.** Convertir la propuesta revisada en `constitution.md`, conservando la separación entre principios y procedimientos, sin añadir decisiones ni generar código.

**Fundamento y finalidad pedagógica.** En 2.º DAM el contrato de trabajo se aprueba antes de ejecutarse. Separar «principios» (qué se cumple siempre) de «procedimientos» (cómo se aplica) permite distinguir el estándar de la receta. Es el equivalente a aprobar un esquema antes de soldar: el esquema no es el cableado, pero lo condiciona.

**Contexto.** Fase de planificación en `main`, sin SPEC ni código. Se pasó de agente Plan a Build en la misma sesión, sin `/new`. El árbol ya estaba sucio por artefactos preexistentes (`README.md` modificado y varios archivos sin seguimiento); este paso añadió además `constitution.md`. Skills cargadas: `documentar` para este registro; no se cargaron otras en el paso documentado. Artefactos consultados: `AGENTS.md`, el borrador inicial de `constitution.md`, el `constitution.md` ya escrito y solo el final de `docs/DESARROLLO.md` para numeración. No hay integración remota, por lo que no aplica aún rama documental ni PR; si el registro debe incorporarse al repositorio más adelante, se hará en rama documental con PR autorizado, o el profesor lo conservará fuera del repositorio hasta la siguiente rama funcional.

**Prompts usados y aclaraciones.**
1. «Propón constitution.md para una práctica de 2.º DAM con SDD, EARS, Given–When–Then, TDD Red–Green–Refactor, arquitectura deducida, simplicidad, separación, seguridad, regresión, trazabilidad, aprobación humana y Git por funcionalidad»; con restricciones de C#/.NET 10, WPF con XAML y code-behind sin MVVM, JSON local, xUnit y lógica independiente de WPF y del disco; planificación en `main`, después ramas, merge fast-forward, pruebas y PR revisado; autorización por operación Git/GitHub; diferencia principios de procedimientos, pregunta ambigüedades y no escribas archivos ni código. (Resumen fiel del prompt original.)
2. Respuestas a las seis aclaraciones: «PR → merge → tests → push»; «Anexo en constitution.md»; «Crear ramas, Commits, Push, Crear o actualizar PR, Merge local y push final»; «Core + App + Tests»; «Sí, con autorización»; «Sí, al cambiar a Build».
3. «La propuesta ha sido revisada y aprobada. Guarda exclusivamente el texto aprobado en las rutas indicadas. Solicita autorización antes de escribir; no añadas decisiones ni generes código. Destino: constitution.md.»
4. Autorización para escribir: «Sí, texto literal».
5. «Carga la skill documentar y documenta el paso que acabamos de realizar. Presenta la propuesta y espera autorización antes de añadirla.»

«Sí, texto literal» se interpretó como conservar incluso el encabezado «pendiente de aprobación del texto final». «Sí, al cambiar a Build» autorizó escribir el archivo, no hacer commits.

**Proceso.** En Plan se propuso un borrador en dos secciones y se formularon seis preguntas; con las respuestas se ajustó a la v0.2 y se entregó el texto íntegro en la conversación. Tras el cambio a Build y la aprobación humana se pidió autorización explícita indicando comando, destino y motivo; se escribió `constitution.md` y se confirmó el resultado. Ahora se propone este registro. No se generó código, no se hicieron commits ni operaciones remotas.

**Decisiones y alternativas.** Decisiones humanas: orden PR → merge local `--ff-only` → pruebas → push; procedimientos como anexo en el mismo archivo; autorización individual para crear rama, commit, push, PR, merge y push final; estructura `Core`/`App`/`Tests`; planificación en `main` con commit previa autorización; escritura literal del texto aprobado. Alternativa descartada: cambiar el encabezado a «aprobado», por la instrucción de no añadir decisiones. Alternativa pendiente: el commit de los artefactos de planificación en `main`.

**Responsabilidad.** El agente propuso, preguntó y escribió solo `constitution.md` tras autorización; el humano revisó, aprobó y autorizó. Este registro, si se autoriza, se añadirá al final de `docs/DESARROLLO.md` conservando intactas las líneas 1-39. No se modifica ningún otro archivo.

**Comandos y resultados reales.**
- Herramienta `write` sobre `constitution.md` → «Wrote file successfully: constitution.md».
- `Get-Content -Tail 60` y `-Tail 24` → salida con caracteres mal codificados en consola; `(Get-Content -Encoding utf8).Count` → `39`; herramienta `read` (líneas 1-39) → numeración correcta, última sección `## 1. ...`.
- `git status --short --branch` → `## main...origin/main`, ` M README.md`, `?? .github/`, `?? .opencode/`, `?? AGENTS.md`, `?? constitution.md`, `?? docs/`, `?? opencode.json`, `?? prd.md`, `?? templates/`.
- Herramienta `question` (ambigüedades y autorización) → respuestas humanas indicadas arriba.
- No consta `git commit`, `git push`, `gh pr create` ni `dotnet test`.

**Errores y resolución.** La lectura por consola con `Get-Content` sin codificación mostró caracteres mal codificados, igual que en el registro 1; se resolvió contando con `-Encoding utf8` y leyendo el final con la herramienta `read`, sin modificar el archivo. No hubo fallos al escribir `constitution.md`.

**Conceptos aprendidos y punto de control.** Una constitución no es código: fija criterios y formas de trabajo antes de que exista una SPEC o una prueba; separar principios de procedimientos evita confundir el «qué» con el «cómo». Ejemplo de 2.º FP: antes de montar un sensor se firma el esquema de cableado; cambiar el esquema después exige aprobación, igual que cambiar un principio. Punto de control: no escribir ni hacer commit sin autorización explícita; el texto aprobado se guardó literal y el registro solo se añade tras aprobación.
