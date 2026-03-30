# Documentación en repos con IA: guía operativa

[← Volver al capítulo *Ingeniería de Contexto*](../ingenieria-de-contexto.md)

---

## 1. Documentación para humanos vs. documentación para IA

### Qué tipo de información pertenece a cada una

**Para humanos:**
- Contexto de negocio: por qué existe el proyecto, qué problema resuelve
- Guías de onboarding: cómo configurar el entorno, cómo correr el proyecto
- Decisiones de arquitectura y sus trade-offs (ADRs)
- Flujos de trabajo del equipo: branching strategy, proceso de PR, convenciones de commit

**Para IA:**
- Restricciones explícitas: qué puede y no puede modificar un agente
- Mapa de módulos: qué hace cada carpeta y cada archivo principal
- Convenciones de código que no son inferibles desde el código mismo
- Ejemplos de input/output de funciones críticas
- Invariantes del sistema: relaciones entre componentes que deben mantenerse

La diferencia operativa: la doc humana puede omitir lo obvio; la doc para IA no puede omitir nada que no esté en el código.

### Dónde debe vivir dentro del repo

```
/docs/          → documentación para humanos
/ai/            → contexto operativo para agentes
README.md       → punto de entrada único (sirve a ambos)
AGENTS.md       → instrucciones directas para agentes IA (raíz del repo)
```

Regla: si el documento lo leerá principalmente un humano para entender el sistema, va en `/docs`. Si lo consumirá un agente para actuar sobre el código, va en `/ai`.

### Convenciones de naming y formato

| Tipo | Formato | Extensión | Ejemplo |
|------|---------|-----------|---------|
| Doc humana | Prosa + Markdown | `.md` | `docs/arquitectura.md` |
| Contexto de agente | Listas estructuradas | `.md` | `ai/contexto-modulos.md` |
| Prompts del sistema | Texto plano o YAML | `.md` / `.yaml` | `ai/prompts/revisor-pr.md` |
| Ejemplos para IA | JSON o Markdown | `.json` / `.md` | `ai/examples/formato-commit.json` |
| Reglas de editor IA | Formato propio | `.mdc` | `.cursor/rules/general.mdc` |

Naming: usar kebab-case en todo. Sin espacios, sin mayúsculas en nombres de archivo.

### Sincronización en el flujo de trabajo con Git

La documentación muere cuando no está en el mismo flujo que el código. Regla operativa:

- **Cambio en código → PR incluye actualización de doc afectada.** Si cambia una interfaz pública, cambia su entrada en `/ai/contexto-modulos.md`.
- **Plantilla de PR con checklist:** incluir ítem explícito "¿Actualicé `/ai/` si aplica?"
- **Los prompts y el contexto de IA se versionan igual que el código.** Cada cambio en `ai/` tiene su propio commit con mensaje semántico.
- No usar wikis de GitHub para contexto crítico de agentes: no están en el árbol de Git y se desincronizarán.

---

## 2. README como punto de entrada del repositorio

### Qué es el README

El README es el primer archivo que lee cualquier persona o agente que llega al repositorio. Es el contrato de orientación del proyecto: en 2 minutos debe quedar claro qué hace el sistema, cómo correrlo y dónde encontrar el resto de la información.

No es documentación exhaustiva. No es un manual de usuario. No es un changelog. Es un índice ejecutable: lo suficiente para que un desarrollador nuevo pueda moverse solo, y lo suficiente para que un agente IA pueda orientarse sin ambigüedad.

Un README mal mantenido genera más fricción que no tener README. Si no puedes comprometerte a mantenerlo sincronizado con el código, mantenlo mínimo.

### Qué no es el README

- **No es una wiki.** El contexto profundo va en `/docs/`. El README enlaza, no duplica.
- **No es un pitch de ventas.** Si necesita convencer, está mal enfocado.
- **No es el lugar para instrucciones de producción.** Eso va en `/docs/deploy.md`.
- **No es un changelog.** Para eso existe `CHANGELOG.md`.
- **No es estático.** Cada cambio que afecte instalación, estructura o contratos debe reflejarse en el README en el mismo PR.

### Estructura propuesta

Hemos construido una plantilla que cubre las mejores prácticas consolidadas para proyectos de software con componentes de IA. No es la única estructura válida, pero es sólida y probada. Está organizada en dos audiencias explícitas dentro del mismo archivo:

**Bloque de orientación rápida** — para cualquiera que llegue al repo:
- Badges funcionales (build, coverage, versión, estado) — solo si están conectados a CI real
- Una línea de descripción: qué hace y para quién
- Quick Start con el comando mínimo para levantar el sistema
- Tabla de troubleshooting con los errores más comunes

**Bloque para usuarios** — contexto de producto:
- Problema, solución y por qué importa
- Casos de uso concretos
- Features principales y diferenciadores
- Demo o capturas de pantalla si existen

**Bloque para desarrolladores** — contexto técnico:
- Tech stack con justificación por capa (no solo lista de tecnologías)
- Instalación con requisitos exactos y variables de entorno
- Ejemplo de uso de API
- Diagrama de arquitectura de alto nivel con enlace a `/docs/architecture.md`
- Comandos de testing

**Bloque de contribución y estado**:
- Pasos para contribuir y contactos clave
- Estado del proyecto (MVP / Beta / Producción)
- Índice de documentación: tabla con todos los docs relevantes y sus rutas
- Licencia

La plantilla completa, lista para copiar y adaptar, está en [`README-template.md`](./README-template.md).

### Optimización para nuevos desarrolladores y para agentes IA

**Para desarrolladores nuevos:**
- El Quick Start debe funcionar en cero contexto previo, en un entorno limpio
- Especificar versiones exactas de runtime, no rangos vagos ("Node >= 18", no "Node moderno")
- Indicar qué esperar al terminar la instalación: URL, puerto, credenciales de prueba
- La tabla de troubleshooting elimina el 80% de las preguntas repetidas en onboarding

**Para agentes IA:**
- El índice de documentación al final es crítico: permite al agente navegar el repo sin exploración ciega
- El tech stack con justificaciones contextualiza decisiones que no son inferibles desde el código
- Mantener el árbol de carpetas actualizado; los modelos lo usan para orientarse antes de leer código
- El enlace explícito a `AGENTS.md` y `/ai/` debe estar presente; no asumir que el agente lo encontrará por su cuenta

---

## 3. Estructura de carpetas en GitHub

### Propuesta de organización

```
├── README.md
├── AGENTS.md              # instrucciones para agentes IA (raíz obligatoria)
├── CONTRIBUTING.md
├── .gitignore
├── .env.example
│
├── src/                   # código fuente
├── docs/                  # documentación para humanos
├── ai/                    # contexto operativo para agentes
├── config/                # configuración de herramientas y entorno
├── scripts/               # automatizaciones y utilidades
└── tests/                 # tests (si no están colocados junto al src)
```

### Propósito de cada carpeta

**`/src`**
Código fuente únicamente. Sin documentación narrativa, sin scripts de utilidad. Si el proyecto tiene múltiples servicios, subdividir: `src/api/`, `src/worker/`, `src/shared/`.

**`/docs`**
Documentación para desarrolladores humanos: arquitectura, decisiones de diseño (ADRs), guías de despliegue, diagramas. Formato Markdown. Versionada en Git. No incluir aquí contexto para agentes.

**`/ai`**
Todo lo que un agente necesita para operar sobre este repo:

```
ai/
├── context/               # descripción de módulos, contratos, invariantes
│   ├── modulos.md
│   └── invariantes.md
├── prompts/               # prompts del sistema reutilizables
│   ├── revisor-pr.md
│   └── generador-tests.md
└── examples/              # ejemplos de input/output para calibrar modelos
    └── formato-commit.json
```

**`/config`**
Configuración de herramientas del proyecto: linters, formateadores, CI/CD, variables de entorno de referencia. No mezclar con `src/`.

```
config/
├── eslint.config.js
├── prettier.config.js
└── ci/
    └── pipeline.yaml
```

**`/scripts`**
Scripts de automatización que no son parte del producto: seeds de base de datos, migraciones manuales, utilidades de deploy, generación de fixtures. Documentar brevemente cada script con un comentario en la primera línea.

### Qué versionar vs. ignorar

**Versionar siempre:**
- Todo lo de `/ai/` — los prompts y el contexto son activos del proyecto
- `.env.example` — con claves reales vacías, como referencia
- Configuraciones de herramientas (`eslint`, `prettier`, `tsconfig`)
- Archivos de CI/CD

**Ignorar siempre:**
```gitignore
.env                    # variables reales
node_modules/
dist/
build/
*.log
.DS_Store
coverage/
```

**Ignorar, pero con criterio:**
- Archivos generados (`dist/`, `build/`): ignorar si el proceso de build es parte del CI
- Dependencias de IA locales (modelos descargados, embeddings): ignorar, documentar cómo obtenerlos

---

## 4. Gestión de contexto para IA dentro del repo

### Dónde almacenar cada tipo de artefacto

| Artefacto | Ubicación | Notas |
|-----------|-----------|-------|
| Instrucciones globales para agentes | `AGENTS.md` (raíz) | Leído automáticamente por Codex y similares |
| Instrucciones por directorio | `AGENTS.md` dentro de cada subcarpeta | Aplican solo al scope de esa carpeta |
| Reglas de editor IA (Cursor, etc.) | `.cursor/rules/` | No afectan a otros entornos |
| Prompts del sistema reutilizables | `ai/prompts/` | Un archivo por prompt, con nombre descriptivo |
| Ejemplos de calibración | `ai/examples/` | JSON o Markdown estructurado |
| Contexto de módulos | `ai/context/modulos.md` | Mapa actualizable del proyecto |

### Cómo versionar contexto de IA en Git

Los artefactos de IA cambian junto con el código. Tratar los cambios en `/ai/` igual que los cambios en `/src/`:

- Commit atómico: si cambia una función pública, el mismo commit actualiza su entrada en `ai/context/modulos.md`
- Mensaje de commit semántico para cambios de contexto:
  ```
  docs(ai): actualizar invariante de módulo de pagos tras refactor
  ```
- En PRs que afecten APIs o contratos internos, el reviewer verifica que `/ai/context/` esté actualizado

### Cómo estructurar archivos para que sean consumibles por humanos y máquinas

Un archivo de contexto bien estructurado sigue esta convención:

```markdown
# Módulo: Pagos

## Responsabilidad
Procesa transacciones y emite eventos al bus interno. No accede directamente a la base de datos de usuarios.

## Contratos
- Input: `PaymentRequest` (ver `src/payments/types.ts`)
- Output: evento `payment.processed` en el bus

## Restricciones
- No modificar `PaymentProcessor` sin actualizar los tests de integración en `tests/payments/`
- El timeout máximo de transacción es 30s; no incrementar sin aprobación de arquitectura

## Archivos clave
- `src/payments/PaymentProcessor.ts` — lógica principal
- `src/payments/types.ts` — contratos de tipos
- `tests/payments/integration.test.ts` — tests de integración
```

Este formato es legible para un humano y estructurado suficientemente para que un agente lo parsee sin ambigüedad.

### Estrategias para evitar degradación del contexto

- **Anclar el contexto al código:** en lugar de describir comportamientos en prosa, referenciar el archivo y la línea cuando sea posible
- **Fechas de revisión:** incluir un campo `<!-- última revisión: YYYY-MM-DD -->` al inicio de cada archivo de contexto
- **Revisión periódica:** agregar una tarea recurrente al proceso del equipo para auditar `/ai/context/` cada sprint o cada release mayor
- **Prohibir contexto duplicado sin referencia cruzada:** si un concepto está en dos archivos, uno debe ser la fuente de verdad y el otro debe enlazarlo explícitamente

---

## 5. Principios operativos en GitHub

### Commits claros y semánticos

Formato: `tipo(scope): descripción en imperativo`

| Tipo | Cuándo usarlo |
|------|--------------|
| `feat` | Nueva funcionalidad |
| `fix` | Corrección de bug |
| `refactor` | Cambio sin nuevo comportamiento |
| `docs` | Cambios en `/docs/` o README |
| `docs(ai)` | Cambios en `/ai/` |
| `test` | Añadir o corregir tests |
| `config` | Cambios en `/config/` o CI |
| `chore` | Mantenimiento sin impacto en producto |

Un commit que cambia código y no actualiza la documentación afectada es un commit incompleto.

### Pull Requests como unidad de revisión

Un PR debe ser revisable en menos de 30 minutos. Si es más grande, dividirlo.

**Plantilla mínima de PR:**

```markdown
## Qué cambia
(Una o dos líneas)

## Por qué
(Contexto necesario para el reviewer)

## Checklist
- [ ] Tests actualizados o añadidos
- [ ] `/docs` actualizado si aplica
- [ ] `/ai/context/` actualizado si cambia algún contrato o módulo
- [ ] `.env.example` actualizado si hay nuevas variables
```

### Documentación como parte del código

No es opcional ni se hace "después". Las reglas operativas:

- Un PR que añade un endpoint público sin actualizar su contrato en `/ai/context/` no pasa review
- Los ADRs (Architecture Decision Records) se escriben en el PR que implementa la decisión, no retroactivamente
- Los comentarios en código son para el *por qué*, no para el *qué*. El *qué* debe ser legible desde el código mismo

### Relación entre código, docs y contexto IA en cada cambio

Cada cambio significativo toca tres capas:

```
Cambio en código (src/)
    └── Doc humana actualizada (docs/) — si cambia arquitectura o flujo
    └── Contexto de IA actualizado (ai/context/) — si cambia un módulo o contrato
```

No todos los cambios requieren las tres capas. Un fix de bug interno no necesita actualizar docs ni contexto. Un refactor que cambia una interfaz pública sí requiere las tres.

---

## 6. Criterios de calidad del repositorio

### Qué debe poder hacer un tercero al clonar el repo

**Entender el proyecto** (en menos de 5 minutos):
- Leer el README y tener claro qué hace, qué tecnologías usa y cómo está organizado
- Encontrar el contexto de IA sin buscar

**Correrlo localmente** (en menos de 15 minutos):
- Seguir los pasos del README sin consultar a nadie ni buscar documentación adicional
- Ver el sistema funcionando con datos de prueba si los hay

**Ubicar el contexto de IA** (inmediatamente):
- `AGENTS.md` en la raíz es el punto de entrada
- `/ai/` contiene el resto, con estructura autoexplicativa

### Checklist de validación del repositorio

**Estructura y navegabilidad**
- [ ] README tiene descripción de una línea, requisitos, comandos y árbol de carpetas
- [ ] Existe `AGENTS.md` en la raíz con instrucciones para agentes
- [ ] Existe `/ai/context/` con descripción actualizada de módulos principales
- [ ] No hay documentación crítica fuera del árbol de Git (sin wikis, sin Notion como fuente de verdad)

**Reproducibilidad**
- [ ] Los comandos del README funcionan en un entorno limpio
- [ ] `.env.example` existe y tiene todas las variables requeridas con comentarios
- [ ] El `.gitignore` excluye secretos, builds y dependencias, pero no contexto de IA

**Sincronización código-docs-IA**
- [ ] Los módulos principales tienen entrada en `/ai/context/`
- [ ] No hay referencias a rutas o nombres de archivos que ya no existen
- [ ] Los prompts en `/ai/prompts/` coinciden con la funcionalidad actual del sistema

**Flujo de trabajo**
- [ ] Los commits siguen convención semántica
- [ ] La plantilla de PR incluye ítem de actualización de `/ai/`
- [ ] Los ADRs existen para las decisiones de arquitectura no obvias

---

*Este documento es parte del manual de Ingeniería de Contexto. Se actualiza cuando cambia la estructura del repositorio o el flujo de trabajo del equipo.*
