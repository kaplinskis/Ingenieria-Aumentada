# Documentación para humanos vs. contexto para IAs

[← Volver al capítulo *Ingeniería de Contexto*](../ingenieria-de-contexto.md)

La misma pieza de texto rara vez sirve por igual a una persona que aprende el sistema y a un modelo que debe **actuar** dentro de reglas acotadas. Este documento detalla la distinción, los trade-offs y patrones prácticos.

## Objetivos distintos

| | Documentación para humanos | Contexto para IAs |
|---|---------------------------|-------------------|
| **Propósito** | Entender, recordar, alinear equipos | Reducir espacio de soluciones, fijar supuestos ejecutables |
| **Éxito** | Claridad narrativa, ejemplos, “por qué” | Precisión, consistencia, estructura repetible |
| **Lectura** | Escaneo, saltos, intuición | Secuencial o por trozos; sensible a ambigüedad y contradicciones |
| **Vida útil** | Puede envejecer con gracia si la historia sigue siendo válida | Lo obsoleto se interpreta como vigente: alto riesgo |

No son opuestos excluyentes: a menudo **comparten fuente** (misma decisión, mismo contrato), pero el **formato y el nivel de detalle** deben ajustarse al consumidor.

## Qué prioriza cada una

**Humans-first** tiende a:

- Historias de usuario, diagramas, analogías, enlaces contextuales.
- Omisiones deliberadas (“los detalles están en el código”) que un humano tolera.
- Tono y voz de marca; redundancia pedagógica.

**IA-first** tiende a:

- Listas explícitas: permitido / prohibido, rutas de archivos, nombres de comandos.
- Definiciones sin sinónimos contradictorios (una sola forma de llamar al mismo concepto).
- Invariantes y límites: “nunca tocar X sin actualizar Y”.

## Anti-patrón: un solo documento “para todo”

Un README larguísimo que mezcla onboarding emocional, chistes internos y reglas estrictas para agentes **confunde al modelo** y **fatiga al humano**. Mejor:

- Mantener la **narrativa humana** donde el equipo ya la busca (wiki, README de alto nivel).
- Colocar el **contexto operativo para agentes** en artefactos explícitos: `.cursor/rules`, `AGENTS.md`, plantillas de PR, `docs/...` versionados y referenciados desde el flujo de trabajo.

## Cuándo duplicar (consciente) vs. enlazar

- **Duplicar** solo cuando la formulación debe cambiar (misma idea, distinta redacción). Anotar en ambos sitios que son facetas del mismo contrato, o generar un **único origen** (por ejemplo esquema OpenAPI) y derivar texto humano desde ahí.
- **Enlazar** cuando el humano necesita profundidad opcional y la IA necesita un extracto estable: el contexto para la IA puede ser un resumen de 30 líneas con enlace al doc largo *solo si* el agente puede recuperar ese enlace (RAG, fetch); si no, el resumen ejecutable debe ser autocontenido.

## Checklist rápido

- [ ] ¿Las reglas críticas para la IA están en bullets inequívocos, no solo en párrafos narrativos?
- [ ] ¿Los nombres de módulos, carpetas y comandos coinciden literalmente con el repo?
- [ ] ¿Hay contradicciones entre README, reglas del editor y comentarios en código?
- [ ] ¿La doc humana indica *dónde* vive el contexto oficial para agentes?

## Referencias

*(Enlazar aquí otros apartados del manual cuando existan: especificaciones legibles por máquina, trazabilidad, etc.)*
