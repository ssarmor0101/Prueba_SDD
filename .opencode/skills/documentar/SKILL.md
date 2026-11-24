---
name: documentar
description: Registrar retrospectivamente un paso realizado y verificado en docs/DESARROLLO.md, con finalidad pedagógica y aprobación humana.
---
# Documentación retrospectiva
Solo por petición explícita, en Build y sin /new desde la sesión que se documenta. Consultar únicamente el final del fichero para numeración; nunca usarlo como contexto técnico. Presentar propuesta y esperar autorización antes de añadir al final. No reescribir entradas previas. No modificar otros archivos ni hacer commits por iniciativa propia.

Cada entrada incluye, cuando corresponda: número y título; objetivo; fundamento teórico y pedagógico; SPEC, rama, agente(s), uso de /new, skills y artefactos consultados; prompts realmente usados y aclaraciones; explicación del proceso; decisiones humanas y alternativas; archivos y responsabilidad; comandos y resultados reales; errores y resolución; conceptos aprendidos y punto de control. Explicar por qué, distinguir propuesta de decisión, incluir ejemplos útiles de nivel 2.º FP. Omitir apartados irrelevantes. No inventar ejecuciones ni reproducir conversaciones completas. Excluir credenciales, tokens, hashes, salts y datos personales. Si falta evidencia, indicar que no consta. Comprobar que el contenido anterior permanece intacto.

El registro no sustituye spec, plan, tasks ni verification. Durante el ciclo TDD documentar tras Refactor/regresión, sin interrumpir Red–Green. Tras integración remota, registrar el resultado real en una rama documental con PR autorizado si se necesita incorporar la entrada al repositorio: no dejar main local sucia ni publicar main directamente tras la línea base. Alternativamente el profesor conserva esa entrada fuera del repositorio hasta la siguiente rama funcional; para la última usar PR documental.
