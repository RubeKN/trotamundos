# Resumen paper "Improving LLM-assisted code generation through the use of architectural documents and implementation plans"

Generar codigo con lenguaje natural puede producir arquitecturas fragiles e incompletas. El paper muestra como un uso estructurado de documentos de arquitectura y planes de implementacion mejoran la correccion funcional y modularidad del codigo generado por LLMs.

- El documento de arquitectura como input es fundumental. Sin el, ignora patrones limpios y genera estructuras caoticas
- El plan de implementacion explicito eleva las probabilidad de que el codigo cumpla los casos de uso complejos

## Recomendaciones del paper
- Crear un `implementationPlan.md`, con el documento de `Architecture.md`, se pide al LLM que analice las especificaciones y proponga un plan dividido en fases logicas con objetivos, actividades y entregables por cada fase
- No pedir que cree todo el sistema en una ejecucion, aprovechar las fases del plan de ejecucion para que se genere fase a fase verificando y corriendo pruebas al finalizar cada etapa antes de seguir con la siguiente
- La revision humana es importante para corregir nombres, completar logica y asegurar trazabilidad con el diseño

## Prompt para generar el plan de implementación

```text
Please review the documentation in the following files @requirements.md @architectureDesign.md I would like you to propose an implementation plan for the design and requirements that you have just read. Create an implmentationPlan.md document where you describe how you will implement these specifications. The plan should describe a number of phases and each phase should include the main objective, a number of activities and tasks and deliverables associated to the phase.
```

## Prompt para iniciar la codificación por fases
```
Consider the @requirements.md for this system and the @implementationPlan.md. Let’s generate the code for this application, we will proceed phase by phase of the implementation plan, let’s start with phase 1.
```