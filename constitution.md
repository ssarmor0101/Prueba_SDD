# Constitución — propuesta v0.2 (pendiente de aprobación del texto final)

Estado: propuesta ajustada con las decisiones humanas. No entra en vigor hasta
aprobación explícita del texto. Autor y fecha: pendientes.

## A. Principios (norma estable)

**P1. Especificar antes de construir (SDD).**
No se escribe código de producción sin PRD, especificaciones EARS, criterios
Given–When–Then, arquitectura deducida, plan y tareas aprobados. La aprobación
de esos cinco artefactos es requisito previo a cualquier implementación.

**P2. Requisitos y aceptación verificables.**
Los requisitos se expresan en EARS (ubiquitous, event-driven, state-driven,
unwanted, optional). Cada requisito se concreta en escenarios
Given–When–Then ejecutables como pruebas xUnit. Se rechazan criterios ambiguos.

**P3. Arquitectura deducida y simplicidad.**
La estructura se deduce de las restricciones: tres proyectos como mínimo —
`Core` (biblioteca `net10.0`, lógica e interfaces; sin WPF y sin acceso a
disco), `App` (WPF, XAML + code-behind, sin MVVM) y `Tests` (xUnit). No se
añaden capas, proyectos ni dependencias especulativas. Prevalece YAGNI.

**P4. Separación de responsabilidades.**
La lógica de negocio reside en `Core`, independiente de WPF y de la E/S. `App`
solo presenta, delega y contiene la implementación concreta del repositorio
JSON. `Tests` sustituye esa persistencia por un doble en memoria.

**P5. TDD Red–Green–Refactor.**
Toda funcionalidad comienza con una prueba que falla por la razón esperada
(Red), sigue con la implementación mínima (Green) y termina con Refactor con la
suite en verde. Toda excepción requiere autorización explícita y documentada.

**P6. Calidad y regresión.**
La suite completa de xUnit pasa en la rama antes del PR y de nuevo tras el
merge local, antes del push a `main`. Ningún cambio rompe pruebas existentes;
una regresión bloquea la integración hasta corregirse.

**P7. Seguridad.**
Validación de entradas, `System.Text.Json` sin resolución de tipos
arbitrarios, ruta del JSON controlada y relativa a una ubicación conocida,
ausencia de secretos o credenciales en el repositorio y superficie de archivos
mínima.

**P8. Supervisión humana y trazabilidad.**
Toda escritura de archivos y toda operación Git/GitHub de escritura requieren
autorización previa y explícita, mostrando comando, destino y motivo. Se
registran decisiones, aprobaciones y su correspondencia con requisitos. Ante
duda o conflicto, se detiene el trabajo y se pregunta.

**P9. Integración controlada.**
`main` solo recibe cambios revisados. El trabajo se realiza por funcionalidad
en ramas, con PR remoto revisado, merge local *fast-forward* y verificación
antes del push final.

**P10. Modificación de la constitución y conflictos.**
Esta constitución prevalece sobre PRD, especificaciones y código. Cambiarla
requiere propuesta, aprobación y nueva versión. Ante conflicto entre documentos
se aplica esta precedencia y se documenta la resolución.

## B. Anexo de procedimientos (forma de aplicar los principios; revisable con aprobación)

**Proc-0.** Las propuestas aprobadas se guardan antes de cambiar de agente o
ejecutar `/new`. La escritura se hace en Build, en la misma sesión, y solo con
autorización.

**Proc-1. Planificación en `main`.** Se escriben y se commitean en `main`, con
autorización previa, los artefactos: PRD → especificaciones EARS → criterios
Given–When–Then → arquitectura deducida → plan y tareas. Solo después se crean
las ramas de funcionalidad. Sin código hasta aprobar los cinco artefactos.

**Proc-2. Ciclo por funcionalidad.** Rama `feature/<id-REQ>` → ajuste de
EARS/GWT de la funcionalidad → Red → Green → Refactor → suite completa en la
rama → commit → push → PR → revisión → `git merge --ff-only` en `main` → suite
completa en `main` → push de `main`.

**Proc-3. Autorización Git/GitHub.** En Build se pide permiso por cada una de
estas operaciones, indicando comando, destino y motivo: (1) crear rama,
(2) commit, (3) push de rama, (4) crear/actualizar PR, (5) merge local
`--ff-only`, (6) push de `main`. Sin autorización no se ejecuta la operación.

**Proc-4. Trazabilidad.** IDs `REQ-nnn` → `AC-nnn.m` → prueba
`AC-nnn_m_descripcion`. Toda prueba referencia su criterio y todo criterio
referencia su requisito.

**Proc-5. Persistencia y pruebas.** `Core` define el contrato de repositorio;
`App` implementa el repositorio JSON; `Tests` usa `InMemoryRepository`. Las
pruebas unitarias no referencian WPF ni acceden al disco.

**Proc-6. Regresión.** `dotnet test` completo en verde en la rama antes del PR
y de nuevo tras el merge local, antes del push a `main`; un fallo bloquea.

**Proc-7. Límites de contexto.** No se consulta material del profesor ni se usa
`docs/DESARROLLO.md` como contexto técnico. Solo Build, con la skill
`documentar` y aprobación, puede añadir al final un paso realmente realizado.
