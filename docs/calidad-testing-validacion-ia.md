# Calidad, Testing y Validación en Sistemas con IA

Los sistemas donde la IA genera o modifica código, configuración o decisiones operativas introducen nuevos riesgos: alucinaciones, regresiones silenciosas, dependencia de contextos frágiles y superficies de ataque ampliadas. La calidad deja de ser solo “tests verdes” y pasa a incluir **verificación del comportamiento**, **trazabilidad** y **criterios humanos explícitos**.

## Objetivos de este capítulo

- Definir qué significa “correcto” cuando interviene un modelo o un agente.
- Separar **validación automática** (tests, linters, contratos) de **validación humana** (revisiones, criterios de aceptación).
- Proponer prácticas mínimas viables para equipos que usan IA de forma intensiva.

## Dimensiones de calidad

1. **Correctitud funcional**: el sistema cumple los requisitos y casos de uso acordados.
2. **Robustez**: comportamiento predecible ante entradas inesperadas o cambios en dependencias.
3. **Seguridad y privacidad**: no filtrar secretos, no ejecutar acciones no autorizadas, minimizar datos sensibles en prompts y logs.
4. **Mantenibilidad**: código y documentación legibles por humanos; decisiones de diseño recuperables sin depender solo del historial del chat.
5. **Observabilidad**: métricas, logs y trazas que permitan diagnosticar fallos en producción.

## Testing en presencia de IA

- **Tests como contrato**: priorizar pruebas que fijen el comportamiento observable (APIs, CLI, integración) frente a tests frágiles ligados a detalles de implementación generados por el modelo.
- **Pirámide equilibrada**: unitarias rápidas, integración sobre límites reales (BD, colas, HTTP), y un conjunto reducido pero crítico de end-to-end.
- **Datos y fixtures**: versionar datos de prueba representativos; evitar depender de respuestas no deterministas del modelo en la suite principal salvo en tests explícitos de calidad del propio pipeline de IA.
- **Regresión**: cada corrección de un bug debería ir acompañada de un test que lo reproduzca.

## Validación humana y de proceso

- **Definition of Done** que incluya revisión de cambios generados por IA (diff legible, commits atómicos).
- **Checklists** para prompts críticos: alcance, restricciones, formato de salida, criterios de éxito.
- **Revisiones cruzadas** en módulos de alto riesgo (auth, pagos, datos personales).

## Métricas y mejora continua

- Tiempo hasta detectar defectos (shift-left).
- Cobertura de áreas críticas (no solo porcentaje de líneas).
- Incidencias atribuibles a cambios asistidos por IA y lecciones aprendidas documentadas.

## Referencias y lecturas sugeridas

*(Ampliar con enlaces internos del manual o bibliografía cuando existan.)*
