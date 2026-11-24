# Tasks: <feature>
ID, rama, versiones spec/plan, estado, autor, aprobación humana/fecha.
## Preparación y dependencias
## Ciclo C-01: <comportamiento>
Requisitos EARS, criterios, decisiones técnicas, dependencias.
- [ ] SPEC-XXX-T-01 RED: fichero, prueba, fallo esperado, comando, evidencia real, aprobación humana antes de Green.
- [ ] SPEC-XXX-T-02 GREEN: ficheros, depende de T-01, implementación mínima, evidencia de prueba y regresión.
- [ ] SPEC-XXX-T-03 REFACTOR: cambios y motivo (o no procede justificado), evidencia de regresión.
- [ ] Punto de control: revisión humana, git diff, commit ejecutado por Build tras autorización específica (SHA).
Repetir por comportamiento pequeño, no por toda la feature en bloque.
## Tareas de infraestructura/UI
- [ ] SPEC-XXX-T-XX: descripción, requisitos, ficheros, dependencias, método y criterio de finalización.
## Cierre técnico
- [ ] Requisitos y criterios verificados; revisión Plan y correcciones.
- [ ] Compilación, pruebas nuevas y regresión; integración/manuales cuando apliquen.
- [ ] verification.md e índice actualizados con estado técnico real.
La integración local posterior y PR se registran en el PR; no anticipar su estado.
