---
name: tdd
description: Diseñar, ejecutar y revisar TDD con xUnit y regresión.
---

# TDD
Por comportamiento pequeño, vincular requisito y criterio. Usar Arrange–Act–Assert; pruebas deterministas aisladas de WPF, disco y estado compartido. Contratos mínimos compilables permitidos, no lógica adelantada.
RED: escribir prueba, ejecutar y verificar fallo por aserción/comportamiento esperado, no por error de compilación o infraestructura. Registrar comando, nombre, fallo y código de salida. Detenerse y esperar aprobación.
GREEN: implementar mínimo; ejecutar prueba y regresión. Registrar resultados reales. REFACTOR: justificar cambios sin alterar comportamiento, repetir pruebas; justificar si no procede. No cambiar prueba para ocultar defecto. Si prueba ya pasa, investigar si comportamiento existe y registrar, no fingir Red.
Separar integración JSON (archivos temporales y limpieza) de pruebas unitarias, y UI manual. Para infraestructura inicial, comprobar descubrimiento de xUnit con prueba de humo identificada como tal. Cero pruebas descubiertas no cuenta como éxito. No exigir TDD de píxeles o creación de directorios. No registrar credenciales ni hashes/salts.
