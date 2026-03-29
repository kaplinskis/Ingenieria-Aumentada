# Ingeniería de Contexto: Documentación como Interfaz

En equipos aumentados con IA, el **contexto** que recibe el modelo (o el agente) determina en gran medida la calidad de las sugerencias. La documentación deja de ser un archivo estático “para después” y pasa a ser una **interfaz de entrada**: el contrato explícito entre el sistema real, las personas y las herramientas automáticas.

## Qué es la ingeniería de contexto

Es el conjunto de prácticas para **curar, estructurar y mantener** la información que alimenta a la IA: README, ADRs, guías de estilo, esquemas de API, convenciones del repo, reglas del editor y prompts reutilizables. El objetivo es reducir ambigüedad, alinear supuestos y acotar el espacio de soluciones.

## Documentación como interfaz

- **Para humanos**: onboarding rápido, decisiones recuperables y menos reuniones repetitivas.
- **Para la IA**: señales estables (qué está permitido, qué no, cómo se llama algo, dónde vive la lógica crítica).
- **Principio**: lo que no está escrito en un lugar accesible para el flujo de trabajo (repo, reglas del proyecto, plantillas) tiende a **reinventarse** en cada conversación, con inconsistencias.



## Temas avanzados

### 1. El gran cambio de paradigma

La documentación ya no es un entregable pasivo — es una **interfaz activa** entre humanos, sistemas y agentes de IA. Esto cambia su propósito, estructura, nivel de precisión y ciclo de vida completo.

### 2. Documentación para humanos vs. contexto para IAs

La doc humana prioriza narrativa y comprensión; el contexto para IA prioriza **precisión semántica, ausencia de ambigüedad y estructura predecible**. No son lo mismo ni deben mezclarse sin criterio.

**[Desarrollo completo →](ingenieria-de-contexto/humanos-vs-ia.md)**

### 3. El contexto como artefacto de ingeniería

El contexto que consume una IA debe tratarse como código: **versionado, testeado, revisado y mantenido**. Un `CONTEXT.md` mal escrito produce el mismo daño que un bug en producción.

### 4. Confianza y verificabilidad del contexto

¿Cómo sabe la IA — y el humano — que el contexto que consume es confiable, vigente y no fue comprometido? Aquí entran provenance de documentos, firmas, trazabilidad de cambios y la defensa contra **context poisoning** en pipelines automatizados.

### 5. Arquitecturas de contexto

Diseñar cómo se entrega el contexto a los agentes: context windows, RAG, system prompts, embeddings, memoria externa. El ingeniero ahora también diseña **flujos de información hacia la IA**, no solo flujos de datos entre servicios.

### 6. Capas de documentación en un proyecto moderno

Definir las capas coexistentes:

1. Doc humana clásica
2. Contexto operacional para agentes de código
3. Contratos de comportamiento esperado
4. Trazabilidad de decisiones asistidas por IA

### 7. Especificaciones legibles por máquina

OpenAPI, AsyncAPI, JSON Schema y similares dejan de ser opcionales — son el **puente entre lo que el humano diseña y lo que la IA ejecuta**. El objetivo es diseñar specs sobre las que una IA pueda razonar, no solo parsear.

### 8. Documentar el comportamiento esperado, no solo la estructura

Las IAs necesitan saber **qué debe pasar**, no solo qué existe. Precondiciones, postcondiciones, invariantes, casos borde — mucho más cercano a especificación formal que al README tradicional.

### 9. La documentación como fuente de entrenamiento y evaluación

Lo que se documenta hoy puede convertirse en datos de fine-tuning, benchmarks internos o criterios de evaluación para agentes. La calidad de la doc no solo afecta la inferencia actual — **perpetúa comportamientos futuros**. Documentar mal es entrenar mal.

### 10. Trazabilidad y auditoría en sistemas con IA

Cuando una IA asiste o toma una decisión de ingeniería, ¿quedó registrado el contexto que tenía en ese momento? La documentación de proceso ahora incluye **logs de razonamiento y decisiones asistidas** — requisito legal y técnico creciente.

### 11. El ingeniero como curador de contexto

El rol evoluciona: además de escribir código, el ingeniero cuida la **calidad del contexto disponible para los agentes**. Saber qué incluir, qué omitir y cómo estructurarlo es la nueva habilidad crítica del rol.

### 12. Gobernanza y deuda de contexto

Así como existe la deuda técnica, existe la **deuda de contexto**: documentación desactualizada que confunde agentes y produce resultados incorrectos. Estrategias para medirla, priorizarla y pagarla — con la urgencia adicional de que los agentes no distinguen lo obsoleto de lo vigente.
