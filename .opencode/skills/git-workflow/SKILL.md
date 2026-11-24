---
name: git-workflow
description: Gestionar ramas, integración local y pull requests con GitHub CLI, bajo autorización humana.
---
# Git e integración
Plan solo asesora. Build ejecuta exclusivamente operaciones autorizadas. Antes de cada escritura, mostrar comando exacto, destino, motivo y estado; esperar autorización específica y confirmación de herramienta (solo esta vez). Ejecutar un comando por vez; si falla, parar. No leer credenciales ni usar API alternativa para eludir permisos. Comprobar `gh auth status` y repositorio remoto correcto; la autenticación la realiza el humano.

## Línea base documental (antes de implementar)
En main, consolidar gobierno, PRD y luego todas las specs, arquitectura, planes y tareas mediante commits autorizados. Si main no está protegida y es la fase inicial, se permite exclusivamente publicar la línea base documental con `git push -u origin main` tras revisar el diff y obtener autorización específica. Si las reglas remotas lo impiden, trabajar en rama documental y PR, sin desactivar protección. El profesor puede preparar un remoto vacío o clonar el existente; no sobrescribir historial. Tras publicar la línea base, prohibido push directo a main. Confirmar main local y origin/main iguales antes de iniciar implementación.

## Preparación de rama funcional
Comprobar git status, rama, remoto y log sin mostrar credenciales. Comprobar índice aprobado, dependencias integradas, documentación vigente. Desde main limpia y sincronizada, autorizar `git switch main`, `git pull --ff-only origin main` y `git switch -c feature/XXX-nombre` según necesidad. No volver a generar todas las specs; solo revisar la activa y sus dependencias. Si una decisión cambia, detener Build, pasar a Plan y actualizar los documentos afectados previa aprobación en la rama activa. No ampliar alcance sin autorización.

## Commits
Cargar conventional-commits. Revisar cambios, pedir permiso para stage y commit por separado. Un commit Red puede existir en la rama funcional, nunca integrar con pruebas rojas. La evidencia técnica se registra en la rama antes de la integración; no afirmar que el PR ya está fusionado.

## Integración local
Con rama limpia y cambios registrados, comprobar todas las pruebas: `dotnet restore <solución>`, `dotnet build <solución> --no-restore`, `dotnet test <solución> --no-build`. Comprobar códigos de salida y resultados reales; no continuar si faltan pruebas obligatorias o comprobaciones manuales. Actualizar base con `git fetch origin`, `git switch main`, `git merge --ff-only origin/main`, `git switch feature/XXX-nombre`, `git merge main` (cada escritura autorizada). Resolver conflictos solo con aprobación y repetir verificación completa en feature. Registrar SHA probado. Autorizar `git switch main` y `git merge --ff-only feature/XXX-nombre`; repetir todas las comprobaciones. Si fallan, parar y consultar recuperación con profesor, sin reset destructivo. No publicar main. Autorizar `git push -u origin feature/XXX-nombre` únicamente si pasan.

## PR remoto
Mostrar al humano repositorio, base main, head feature, SHA, commits, título y cuerpo basado en `.github/pull_request_template.md`, incluyendo resultados post-merge local. Solicitar autorización separada para crear PR. Ejemplo de una línea (usar valores reales y archivo temporal autorizado o argumento --body):
`gh pr create --base main --head feature/XXX-nombre --title "SPEC-XXX: nombre" --body-file RUTA_TEMPORAL`
Proporcionar URL real. El humano revisa en GitHub (otro revisor si la política lo exige; no autoaprobar). Consultar `gh pr view NUMERO --json state,baseRefName,baseRefOid,headRefName,headRefOid,reviewDecision,mergeStateStatus,statusCheckRollup,url` y checks requeridos. Si cambió base o head, parar y volver a verificar; no improvisar recuperación de main local divergente. Tras revisión y checks requeridos, pedir autorización nueva para `gh pr merge NUMERO --merge --match-head-commit SHA_PROBADO`. No squash/rebase, --admin ni --auto. Si GitHub exige otro método, detenerse y revisar el procedimiento con el profesor. No asumir fusión por el mero éxito de un comando: comprobar estado MERGED.

## Sincronización
Tras fusión real, autorizar `git fetch origin`, `git switch main`, `git merge --ff-only origin/main`; verificar de nuevo `dotnet restore <solución>`, `dotnet build <solución> --no-restore`, `dotnet test <solución> --no-build`, comprobar `git rev-parse HEAD origin/main` (ambos iguales), estado limpio. Eliminar rama local con `git branch -d feature/XXX-nombre` solo previa autorización y si integrada. No iniciar otra SPEC hasta sincronización y revisión. Registrar evidencia posterior al merge en PR mediante comentario autorizado o registro humano; nunca modificar main directamente. No consultar DESARROLLO.md durante Git. La skill documentar gestiona exclusivamente su actualización autorizada. Si el remoto cambia tras la prueba local, detenerse; el profesor decide cómo reconciliar sin operaciones destructivas.
