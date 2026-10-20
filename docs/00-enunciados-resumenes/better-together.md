# Resumen paper "Better Together: An LLM-assisted approach to designing software architectures using Attribute-Driven Design"
Los LLM pueden generar codigo, explicar patrones y proponer componentes, pero para satisfacer los requerimientos importantes de un sistema es mejor cuando siguen una metodologia formal

1. Metodologia explicita: Indicar como es el proceso de ADD
2. Documentacion estructurada: Registrar en un documento que evolucione en cada iteracion
3. Colaboracion: El humano debe revisar decisiones y coregirlas

Pedirle directamente a una IA que diseñe puede
- Omitir requisitos, QAs, decisiones
- Proponer componentes que no encajan entre si o se contradicen
- Falta de justificacion sobre una tecnologia
- Distintas ejecuciones producen distintos resultados
- Falta de detalla

Los autores recomiendan usar un metodo completo y conocido como estructura de trabajo del LLM
- Una descripcion explicida del metodo ADD. Describir los pasos del metodo y las actividades esperadas en cada uno
- Un rol especializado de arquitecto de software
- Un plan inicial de iteraciones
- Un documento arquitectonico unico que se modifica progresivamente
- La ejecucion paso a paso con etapas para que un humano revise

El paso 4-5 de ADD es donde mas valor aporta el LLM, puede desarrollar alternativas, detalalr componentes y producir documentacion de las decisiones. Aunque requiere una buena revision ya que puede ocultar problemas importantes

## Recomendaciones del paper

- Archivo `ArchitecturalDrivers.md` con los drivers priorizados
- Archivo `ADD.md` explicando los pasos formales del metodo
- Configurar el rol para seguir el perfil del arquitecto senior
- Antes de iniciar ADD se hacen 3 actividades
    1. Revisar inputs, el LLM examina el archivo y verifica consistencia de requisitos y comprueba que las prioridades sean comprensibles, si hay ambiguedad debe formular preguntas al usuario
    ```
    Please review the ArchitecturalDrivers.md document and ensure that the requirements are consistent and that you understand the priorities. Ask clarification questions, if needed.
    ```
    2. Crear un modelo de dominio, identifica conceptos principales, relaciones y responsabilidades para incorporar a ARchitecture.md. Diagrama de clases Mermaid y descripcion de elementos
    ```
    Consider the ArchitecturalDrivers.md document and create a domain model for the system. Create this domain model in the Architecture.md document. Represent the domain model using a class diagram using mermaid format. Include a table that describes each element of the domain model.
    ```
    3. Planificar iteraciones, objetivos de cada iteracion y driver que debe atender, guardar en IterationPlan.md
    ```
    Consider the requirement priorities in ArchitecturalDrivers.md and the domain model in Architecture.md. Create an iteration plan for the design of the system, according to the ADD.md process. Describe, for each iteration, what the main goal will be. The first iteration should be focused on initially structuring the system. The following iterations should be focused on addressing high priority drivers. Be sure to address requirements that directly support the business in early iterations. Present the iteration plan as a table with iteration number, goal and list of drivers to be addressed. Output the iteration plan to an IterationPlan.md file in the Design folder.
    ```

## Prompt de rol sugerido por el paper

```
You are Senior Software Architect specialized in cloud-native enterprise systems. Your main goal is to design scalable, secure, and maintainable architectures that align with business goals and real-world constraints such as budget, team size, deadlines, and operational risk.
You must:
- Make architectural recommendations that are technically grounded and context-aware.
- Justify your suggestions using explicit quality attributes (e.g., scalability,performance, cost efficiency).
- Maintain focus on architectural concerns ( domain boundaries, integration patterns, data flow, deployment model, risk).
You cannot:
- Propose solutions that ignore constraints provided by the user (budget, timeline, team capability).
- Make decisions outside the architect’s responsibilities (e.g., procurement, corporate policy).
- Introduce speculative technology with no rationale or clear trade-offs.
Tone and behavior:
- Think like an experienced architect: structured, concise, technical, but not robotic.
- Always explain trade-offs (pros/cons) instead of giving absolute answers.
- Avoid hallucinating: when facts are unknown, ask clarifying questions or state assumptions clearly.
Output expectations:
- Provide architecture-level reasoning, not low-level code unless explicitly requested
- Prefer diagrams and tables for readability. When creating mermaid diagrams, do not put
parentheses inside brackets.
- Follow the ADD process exactly as it is described in the file ADD.md
```