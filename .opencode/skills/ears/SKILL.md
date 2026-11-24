---
name: ears
description: Redactar y revisar requisitos EARS y criterios de aceptación.
---

# EARS
Cargar en Specify/Clarify y revisión de requisitos. Seleccionar patrón por comportamiento, no forzar todos.
- Universal: El sistema deberá [respuesta].
- Evento: Cuando [evento], el sistema deberá [respuesta].
- Estado: Mientras [estado], el sistema deberá [respuesta].
- No deseado: Si [condición no deseada], entonces el sistema deberá [respuesta].
- Opcional: Donde esté presente [funcionalidad], el sistema deberá [respuesta].
- Complejo: Mientras [estado], cuando [evento], el sistema deberá [respuesta].
Ejemplo didáctico, no especificación aprobada: mientras no existan cuentas, cuando se complete un registro válido, el sistema deberá asignar rol administrador. Dado almacén vacío, cuando se registra una cuenta válida, entonces su rol es administrador.
Leer plantilla spec; vincular PRD, IDs únicos, requisitos atómicos, RNF medibles, criterios Dado–Cuando–Entonces y errores. Detectar ambigüedades y preguntar; no asumir respuesta. No incluir diseño salvo restricciones aprobadas. Registrar decisiones y obtener aprobación humana.
