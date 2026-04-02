# Pilar 2 — Proceso de ingeniería e integración de IA

[← Índice de los siete pilares](../siete-pilares-calidad.md)

Este pilar describe cómo el **proceso de desarrollo** y el uso disciplinado de **herramientas de IA** se combinan para sostener la calidad: definición clara de hecho, pruebas por capas, entrega continua, revisión del código generado, patrones de prompts compartidos, conocimiento que sobrevive a los cambios de equipo y bucles de feedback rápidos.

---

## 1. Definition of Done (definición de terminado)

**Cada tarea tiene criterios de finalización explícitos y medibles antes de empezar a trabajar.**

Sin una definición de “hecho” acordada de antemano, el alcance se diluye y la IA (y las personas) optimizan objetivos implícitos equivocados. Los criterios deben ser verificables: qué tests deben pasar, qué documentación mínima actualizar, qué revisión es obligatoria y qué no cuenta como entregable (por ejemplo “código suelto sin integrar”).

---

## 2. Estrategia de pruebas por capas

**Existen pruebas unitarias, de integración y end-to-end en proporciones acordes al perfil de riesgo.**

La pirámide no es decorativa: áreas de alto riesgo o alta complejidad merecen más integración y escenarios extremos; lógica aislada y estable puede vivir con unitarias densas. La proporción se revisa cuando cambia el dominio, el equipo o el uso intensivo de generación automática de código.

---

## 3. Madurez del pipeline CI/CD

**Cada commit se construye, se prueba y es desplegable; los pasos manuales de despliegue se tratan como defectos del proceso.**

El objetivo es reducir la variabilidad entre “en mi máquina funciona” y lo que integra la cadena oficial. Lo manual residual debe estar justificado, documentado y en camino de automatización, no normalizado como costumbre.

---

## 4. Disciplina en el uso de herramientas de IA

**El código generado por IA se revisa con el mismo rigor que el escrito por personas; se entiende lo que se acepta, no solo se copia.**

Diffs legibles, revisión de supuestos, comprobación de licencias y seguridad, y rechazo de cambios opacos forman parte del estándar del equipo. La velocidad de la IA no sustituye la responsabilidad humana sobre lo que entra al repositorio.

---

## 5. Ingeniería de prompts como competencia

**El equipo desarrolla patrones compartidos para consultar las herramientas de IA de forma consistente y efectiva.**

Plantillas, ejemplos de buenos prompts, convenciones de contexto (qué pegar del repo, qué no) y retroalimentación entre pares mejoran resultados más que depender de formulaciones improvisadas en cada conversación.

---

## 6. Mecanismos de transferencia de conocimiento

**Arquitectura, decisiones y patrones quedan documentados en una forma que sobrevive a cambios de equipo.**

ADRs, diagramas mantenidos, guías de onboarding y enlaces canónicos reducen la dependencia de la memoria oral. Lo documentado debe actualizarse cuando cambia el sistema; de lo contrario se convierte en deuda que confunde tanto a humanos como a agentes.

---

## 7. Velocidad del bucle de feedback

**Se minimiza activamente el tiempo entre escribir código y recibir señal de calidad (tests, revisión, señal de producción).**

Cuanto más tarde el feedback, más costoso el arreglo. Acortar el bucle implica CI rápida, revisiones enfocadas, feature flags, observabilidad y cultura de integración frecuente en lugar de lotes grandes.

---

## Relación con el resto del manual

Este pilar conecta con [Calidad, testing y validación en sistemas con IA](../calidad-testing-validacion-ia.md) y con [Ingeniería de contexto](../ingenieria-de-contexto.md): el proceso y la IA solo escalan si el contexto y los criterios de calidad están alineados.

