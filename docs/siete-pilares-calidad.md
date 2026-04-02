# Los 7 Bloques de Calidad en Ingeniería de Software



---

## Bloque 1 — Artesanía del Código
**Riesgo Central si se Descuida:** Base de código imposible de mantener

La artesanía del código es la disciplina de escribir código que comunica la intención con claridad, resiste la entropía con el tiempo y puede ser modificado de forma segura por cualquier miembro del equipo — incluyendo tu yo futuro. Es la base sobre la que dependen todos los demás bloques. Un sistema con artesanía deficiente se degradará independientemente de qué tan bien diseñada esté su arquitectura.

| # | Sub-Punto | Descripción |
|---|---|---|
| 1 | **Claridad en los nombres** | Los nombres de variables, funciones, clases y módulos deben revelar la intención sin necesidad de un comentario o referencia externa. Un nombre es un contrato — le dice al lector qué esperar. |
| 2 | **Responsabilidad de la función** | Cada función realiza exactamente una operación en un nivel de abstracción. Las funciones que hacen múltiples cosas simultáneamente hacen que las pruebas, la depuración y la modificación sean desproporcionadamente más difíciles. |
| 3 | **Control de complejidad ciclomática** | El número de caminos independientes a través de un fragmento de código debe mantenerse bajo. El anidamiento profundo y los condicionales encadenados son síntomas de lógica que no ha sido debidamente descompuesta. |
| 4 | **Disciplina ante la duplicación** | La duplicación no es una preocupación estilística — es una responsabilidad de mantenimiento. Se aplica la Regla de Tres: abstraer en la tercera repetición, no en la primera. La abstracción prematura es tan peligrosa como la duplicación. |
| 5 | **Calidad de los comentarios** | Un comentario que explica *qué* hace el código es una señal de falla — el código debería hacerlo por sí mismo. Un comentario que explica *por qué* se tomó una decisión no obvia es un artefacto de ingeniería de alto valor. |
| 6 | **Formato y estilo consistentes** | La consistencia de estilo es aplicada por herramientas automatizadas, no por convención del equipo ni por el ancho de banda de revisión de código. Cuando un linter o formateador toma la decisión, los ingenieros se enfocan en la lógica. |
| 7 | **Higiene de refactorización** | El código es un artefacto vivo. Cada interacción con un módulo es una oportunidad para dejarlo un poco más coherente. La deuda técnica no es inevitable — es el resultado de elegir no abordar la degradación cuando el costo aún es bajo. |

---

## Bloque 2 — Diseño Arquitectónico
**Riesgo Central si se Descuida:** Resistencia al cambio

El diseño arquitectónico es el conjunto de decisiones estructurales que determinan cómo responde un sistema al cambio — en requerimientos, en escala, en composición del equipo y en tecnología. Una buena arquitectura no predice el futuro; reduce el costo de adaptarse a él. El resultado principal del trabajo arquitectónico no son diagramas, sino decisiones explicitadas.

| # | Sub-Punto | Descripción |
|---|---|---|
| 1 | **Separación de responsabilidades** | Cada capa del sistema tiene una responsabilidad definida y no superpuesta. Cuando las responsabilidades se mezclan, un cambio en un área genera efectos secundarios impredecibles en otra. |
| 2 | **Dirección de dependencias** | Las dependencias apuntan hacia adentro — hacia el dominio — y hacia afuera — hacia la infraestructura — nunca al revés. La lógica de negocio no debe depender directamente de drivers de base de datos, frameworks HTTP o servicios externos. |
| 3 | **Modularidad y cohesión** | Un módulo agrupa todo lo que cambia junto y aísla todo lo que cambia de forma independiente. Alta cohesión dentro del módulo y bajo acoplamiento entre módulos es el ideal estructural. |
| 4 | **Definición de contextos acotados** | El sistema tiene límites explícitos. Cada límite posee su propio modelo de datos, su propio lenguaje y sus propias reglas. La comunicación entre límites es intencional, versionada y mínima. |
| 5 | **Superficie de escalabilidad** | La arquitectura identifica qué componentes están en el camino crítico para escalar y los aísla. No todo escala de igual manera — pretender lo contrario produce sistemas sobreingeniados que no escalan bien en ningún punto. |
| 6 | **Reemplazabilidad** | Cualquier componente de infraestructura — base de datos, broker de mensajes, caché, API externa — puede ser reemplazado sin reescribir la lógica de negocio. Esto se aplica mediante interfaces e inversión de dependencias, no por confianza. |
| 7 | **Registros de Decisiones Arquitectónicas (ADRs)** | Cada decisión de diseño significativa se documenta con su contexto, las alternativas consideradas y la justificación de la elección tomada. Una decisión no documentada será re-debatida o silenciosamente revertida por el próximo ingeniero que la encuentre. |

---

## Bloque 3 — Modelado de Datos y Persistencia
**Riesgo Central si se Descuida:** Degradación de integridad y rendimiento

Los datos sobreviven al código. Los esquemas, relaciones y restricciones definidos tempranamente se vuelven cada vez más costosos de cambiar a medida que el sistema acumula datos y consumidores. Las decisiones de modelado de datos tomadas sin criterio de ingeniería deliberado producen sistemas que parecen saludables y se degradan de forma invisible hasta que se cruza un umbral que requiere una remediación costosa.

| # | Sub-Punto | Descripción |
|---|---|---|
| 1 | **Integridad del esquema** | Las restricciones, tipos de datos, nulabilidad e integridad referencial se aplican a nivel de base de datos. La validación solo a nivel de aplicación es insuficiente — la base de datos es la última línea de defensa para la corrección de los datos. |
| 2 | **Disciplina de normalización** | Los datos se normalizan al nivel apropiado para sus patrones de acceso. La desnormalización es una optimización de rendimiento tomada conscientemente con trade-offs documentados — no una posición predeterminada tomada sin análisis. |
| 3 | **Estrategia de índices** | Los índices existen para servir patrones de consulta específicos, no para cubrir todas las columnas de forma defensiva. El exceso de índices degrada el rendimiento de escritura; la falta de índices degrada el rendimiento de lectura. Ambos son fallas de ingeniería. |
| 4 | **Gestión de migraciones** | Los cambios de esquema son versionados, aplicados de forma incremental, reversibles donde sea posible y ejecutados sin requerir tiempo de inactividad de la aplicación. Una migración es un artefacto de despliegue y debe tratarse con la misma disciplina que el código. |
| 5 | **Definición del ciclo de vida del dato** | Las políticas de retención, archivado y eliminación se definen antes de que se escriba el primer registro. Los datos que se acumulan sin una política de ciclo de vida se convierten simultáneamente en una responsabilidad de cumplimiento, rendimiento y costos. |
| 6 | **Modelo de consistencia** | El sistema elige explícitamente entre consistencia fuerte y eventual por caso de uso. Adoptar uno sin razonar sobre el trade-off es una decisión arquitectónica tomada por accidente. |
| 7 | **Propiedad de las consultas** | Las consultas viven en proximidad a la lógica de dominio que las posee. Las consultas crudas dispersas por capas de servicio, controladores y utilidades indican que la lógica de acceso a datos no tiene dueño y, por tanto, no tiene mantenedor. |

---

## Bloque 4 — Diseño de API y Calidad del Contrato
**Riesgo Central si se Descuida:** Fricción con consumidores y cambios disruptivos

Una API es un contrato publicado para consumidores — internos o externos. Una vez publicado, romper ese contrato tiene un costo que escala con la adopción. La calidad de la API no es estética; determina si los consumidores pueden usar el sistema correctamente, si el sistema puede evolucionar de forma independiente y si los errores pueden diagnosticarse eficientemente.

| # | Sub-Punto | Descripción |
|---|---|---|
| 1 | **Modelado de recursos** | Los endpoints representan recursos de dominio y operaciones con significado semántico claro. Una API que expone detalles de implementación internos — nombres de tablas, llamadas a procedimientos, IDs internos — crea acoplamiento entre consumidores e infraestructura. |
| 2 | **Estrategia de versionado** | Una política de versionado se define antes de que ocurra el primer cambio disruptivo. Versionar después del hecho es reactivo y fuerza decisiones de emergencia bajo presión. La estrategia debe contemplar cómo se comunican, mantienen y deprecan las versiones. |
| 3 | **Consistencia del contrato de errores** | Todas las respuestas de error siguen una estructura uniforme que incluye un código legible por máquina, un mensaje legible por humanos y contexto suficiente para que el consumidor pueda actuar. Los formatos de error inconsistentes obligan a los consumidores a escribir lógica de análisis defensiva. |
| 4 | **Diseño de idempotencia** | Las operaciones de mutación están diseñadas para que ejecutarlas múltiples veces con el mismo input produzca el mismo resultado. Es un requerimiento de confiabilidad, no una optimización — habilita reintentos seguros en entornos distribuidos. |
| 5 | **Validación de entrada en el límite** | Todo el input externo es validado y saneado en la capa de API antes de llegar a la lógica de dominio. El límite es el punto de aplicación — empujar la validación hacia adentro distribuye la responsabilidad y crea brechas. |
| 6 | **Documentación como contrato** | La documentación de la API se genera desde la fuente autoritativa — una especificación OpenAPI, un esquema, una definición de tipos — nunca escrita manualmente y mantenida por separado. La documentación que diverge de la implementación es peor que ninguna documentación. |
| 7 | **Paginación y límites de tasa** | Los endpoints de colección están paginados por defecto desde el primer día. Los límites de tasa son parte del diseño inicial de la API. Ambos son casi imposibles de incorporar de forma limpia una vez que los consumidores han construido contra una API ilimitada y sin restricciones. |

---

## Bloque 5 — Observabilidad y Preparación Operacional
**Riesgo Central si se Descuida:** Operación ciega en producción

Un sistema que no puede observarse no puede entenderse en producción, y un sistema que no puede entenderse no puede depurarse, optimizarse ni operarse de forma confiable. La observabilidad no es monitoreo — el monitoreo te dice cuándo algo está mal; la observabilidad te dice por qué. La preparación operacional es la disciplina de construir sistemas diseñados para fallar con gracia y recuperarse de forma predecible.

| # | Sub-Punto | Descripción |
|---|---|---|
| 1 | **Logging estructurado** | Los logs se emiten en un formato legible por máquina — JSON siendo el estándar — e incluyen un identificador de correlación que vincula una entrada de log a una solicitud u operación específica. Los logs de texto libre no son consultables a escala. |
| 2 | **Instrumentación de métricas** | El sistema expone mediciones cuantitativas de su comportamiento — latencia de solicitudes, tasa de errores, profundidad de cola, throughput. Estas métricas son el vocabulario con el que el sistema comunica su salud. |
| 3 | **Trazabilidad distribuida** | Una solicitud puede seguirse de extremo a extremo a través de todas las capas y servicios que toca. Sin trazabilidad, diagnosticar latencia o fallos en sistemas distribuidos requiere inferencia en lugar de evidencia. |
| 4 | **Umbrales de alerta** | Las alertas se activan cuando el comportamiento visible para el usuario está degradado, no cuando las métricas técnicas internas cruzan umbrales arbitrarios. La fatiga de alertas — causada por alertas que no requieren acción — es en sí misma un riesgo operacional. |
| 5 | **Endpoints de verificación de salud** | El sistema expone endpoints que reflejan su estado operacional real — no solo si el proceso está corriendo, sino si sus dependencias están disponibles y está listo para atender tráfico. |
| 6 | **Disponibilidad de runbooks** | Para cada modo de fallo conocido, existe un procedimiento de recuperación documentado antes de que ese fallo ocurra en producción. Un runbook escrito durante un incidente se escribe bajo las peores condiciones posibles. |
| 7 | **Degradación con gracia** | El sistema define comportamiento explícito para estados de fallo parcial. Cuando una dependencia no está disponible, el sistema tiene una respuesta definida — funcionalidad reducida, resultados en caché o un error claro — en lugar de una cascada de fallos no controlada. |

---

## Bloque 6 — Seguridad y Confiabilidad
**Riesgo Central si se Descuida:** Explotabilidad y fragilidad

La seguridad y la confiabilidad no son características que se agregan a un sistema — son propiedades que deben diseñarse desde el principio. La seguridad es la práctica de reducir la superficie de ataque y limitar el radio de explosión de una brecha. La confiabilidad es la práctica de asegurar que el sistema continúe funcionando correctamente bajo condiciones adversas — carga, fallos y error humano.

| # | Sub-Punto | Descripción |
|---|---|---|
| 1 | **Separación de autenticación y autorización** | La autenticación establece identidad; la autorización determina el permiso. Son mecanismos distintos con modos de fallo distintos. Confundirlos produce sistemas donde el compromiso de uno rompe ambos. |
| 2 | **Principio de mínimo privilegio** | Cada componente, cuenta de servicio y usuario posee solo los permisos estrictamente necesarios para su función. El exceso de privilegio no se convierte en un problema hasta que lo hace — momento en el que el radio de explosión está maximizado. |
| 3 | **Modelado de amenazas en entradas** | Cada punto de entrada al sistema se analiza en busca de vectores de inyección — SQL, comandos, plantillas, path traversal. El modelado de amenazas no es una auditoría puntual; es una práctica que se aplica cuando se introducen nuevos puntos de entrada. |
| 4 | **Gestión de secretos** | Las credenciales, claves API, certificados y tokens nunca aparecen en el código fuente, archivos de log o control de versiones — ni siquiera en ramas de desarrollo. La infraestructura de gestión de secretos se establece antes de que se genere la primera credencial. |
| 5 | **Seguimiento de vulnerabilidades en dependencias** | Las dependencias de terceros se auditan continuamente en busca de vulnerabilidades conocidas. Las dependencias adoptadas en la versión N no permanecen seguras indefinidamente — el panorama de amenazas evoluciona después de la adopción. |
| 6 | **Aislamiento de fallos** | Un fallo en un componente no se propaga sin control a través del sistema. Los circuit breakers, bulkheads y políticas de timeout son decisiones arquitectónicas, no acciones operacionales tardías. |
| 7 | **Objetivos de recuperación** | El Objetivo de Tiempo de Recuperación (RTO) y el Objetivo de Punto de Recuperación (RPO) están definidos, documentados y validados mediante procedimientos de recuperación probados. Una estrategia de respaldo no probada no es una estrategia de respaldo. |

---

## Bloque 7 — Proceso de Ingeniería e Integración de IA
**Riesgo Central si se Descuida:** Ineficiencia compuesta del equipo

El proceso de ingeniería es el sistema por el cual un equipo convierte intención en software funcionando de manera confiable y repetible. En un entorno aumentado con IA, la calidad del proceso determina si la IA acelera al equipo o introduce una nueva categoría de deuda técnica. La integración de la IA en el flujo de trabajo de desarrollo no es automática — requiere disciplina, patrones compartidos y gobernanza explícita para producir resultados netos positivos.

| # | Sub-Punto | Descripción |
|---|---|---|
| 1 | **Definición de terminado** | Cada tarea tiene criterios de completitud explícitos y medibles definidos antes de que comience el trabajo. En flujos de trabajo asistidos por IA, esto es crítico — la IA puede generar outputs que parecen plausibles pero que no satisfacen ningún estándar a menos que el estándar haya sido articulado de antemano. |
| 2 | **Estrategia de pruebas por capa** | Las pruebas unitarias, de integración y de extremo a extremo existen en proporciones calibradas al perfil de riesgo del sistema. En bases de código aumentadas con IA, las pruebas son el mecanismo principal para validar que el código generado se comporta como se pretende, no meramente como se describió. |
| 3 | **Madurez del pipeline CI/CD** | Cada commit se construye automáticamente, se prueba y se coloca en un estado desplegable. Los pasos de despliegue manual se tratan como defectos. En flujos de trabajo aumentados, el pipeline es la puerta de calidad que compensa la confiabilidad variable del código generado por IA. |
| 4 | **Disciplina en el uso de herramientas de IA** | El código, la arquitectura y el contenido generado por IA se revisan con el mismo rigor que los outputs producidos por humanos. El ingeniero es responsable de entender lo que fue generado — aceptar output sin comprensión transfiere la autoría sin transferir la responsabilidad. |
| 5 | **Ingeniería de prompts como habilidad** | Los equipos desarrollan, documentan y comparten patrones para interactuar con herramientas de IA de forma consistente y efectiva. El prompting ad-hoc produce resultados inconsistentes; los patrones de prompt compartidos producen outputs repetibles y revisables. |
| 6 | **Mecanismos de transferencia de conocimiento** | La arquitectura, las decisiones, los patrones y la justificación se documentan de una forma que sobrevive a los cambios de personal. En equipos aumentados con IA, el riesgo del conocimiento implícito se amplifica — la IA puede generar código más rápido de lo que el conocimiento institucional puede socializarse. |
| 7 | **Velocidad del ciclo de retroalimentación** | El tiempo transcurrido entre escribir código y recibir una señal de calidad — desde pruebas, desde revisión, desde producción — se minimiza activamente. Los ciclos de retroalimentación lentos permiten que los defectos se compensen; en flujos de trabajo aumentados con IA, donde el volumen de output es mayor, la retroalimentación lenta es proporcionalmente más peligrosa. |

---

*Ingeniería Aumentada: La Nueva Práctica del Software*
*Marco de Calidad — 7 Bloques × 7 Sub-Puntos*
