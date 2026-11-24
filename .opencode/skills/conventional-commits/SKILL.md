---
name: conventional-commits
description: Proponer, revisar y ejecutar commits autorizados siguiendo Conventional Commits.
---

# Conventional Commits
Formato `tipo(alcance): descripción breve`. Tipos: feat, fix, docs, test, refactor, chore, build. Ejemplos `docs(registration): approve EARS specification`, `test(registration): cover first user role`, `feat(registration): assign role`. Revisar diff y stage selectivo antes de commit; no incluir secretos, datos de usuarios, bin/obj ni archivos ajenos. Red puede registrarse en rama funcional, nunca integrarse hasta Green y regresión. Plan propone únicamente. Build muestra rama, diff, archivos y mensaje; solicita permiso para git add selectivo, revisa git diff --cached y solicita autorización específica para git commit. Tras ejecutar, muestra SHA y estado. No usar git add . indiscriminadamente ; incluir la bitácora únicamente si contiene una entrada retrospectiva aprobada y relacionada con el cambio.
