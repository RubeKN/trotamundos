# Resumen paper "Better Together: An LLM-assisted approach to designing software architectures using Attribute-Driven Design"

Los LLM pueden generar código, explicar patrones y proponer componentes, pero para satisfacer los requerimientos importantes de un sistema es mejor cuando siguen una metodología formal

1. Metodologia explicita: Indicar como es el proceso de ADD
2. Documentación estructurada: Registrar en un documento que evolucione en cada iteración
3. Colaboración: El humano debe revisar decisiones y corregirlas

Pedirle directamente a una IA que diseñe puede

- Omitir requisitos, QAs, decisiones
- Proponer componentes que no encajan entre sí o se contradicen
- Falta de justificación sobre una tecnología
- Distintas ejecuciones producen distintos resultados
- Falta de detalles

Los autores recomiendan usar un método completo y conocido como estructura de trabajo del LLM

- Una descripción explicida del metodo ADD. Describir los pasos del método y las actividades esperadas en cada uno
- Un rol especializado de arquitecto de software
- Un plan inicial de iteraciones
- Un documento arquitectónico único que se modifica progresivamente
- La ejecución paso a paso con etapas para que un humano revise

El paso 4-5 de ADD es donde más valor aporta el LLM, puede desarrollar alternativas, detallar componentes y producir documentación de las decisiones. Aunque requiere una buena revisión ya que puede ocultar problemas importantes

## Recomendaciones del paper

- Archivo `ArchitecturalDrivers.md` con los drivers priorizados
- Archivo `ADD.md` explicando los pasos formales del metodo
- Configurar el rol para seguir el perfil del arquitecto senior
- Antes de iniciar ADD se hacen 3 actividades:
  1. Revisar inputs, el LLM examina el archivo y verifica consistencia de requisitos y comprueba que las prioridades sean comprensibles, si hay ambiguedad debe formular preguntas al usuario
  ```
  Por favor, revisa el documento ArchitecturalDrivers.md y asegúrate de que los requisitos sean coherentes y de que comprendes las prioridades. Si es necesario, pide aclaraciones.
  ```

  2. Crear un modelo de dominio, identificar conceptos principales, relaciones y responsabilidades para incorporar a `Architecture.md`. Diagrama de clases _Mermaid_ y descripción de elementos
  ```
  Analiza el documento ArchitecturalDrivers.md y crea un modelo de dominio para el sistema. Crea este modelo de dominio en el documento Architecture.md. Representa el modelo de dominio mediante un diagrama de clases en formato Mermaid. Incluye una tabla que describa cada elemento del modelo de dominio.
  ```

  3. Planificar iteraciones, objetivos de cada iteración y driver que debe atender, guardar en IterationPlan.md
  ```
    Ten en cuenta las prioridades que figuran en ArchitecturalDrivers.md y el modelo de dominio de Architecture.md. Crea un plan de iteraciones para el diseño del sistema, de acuerdo con el proceso descrito en ADD.md. Describe, para cada iteración, cuál será el objetivo principal. La primera iteración debe centrarse en la estructuración inicial del sistema. Las iteraciones siguientes deben centrarse en abordar los drivers de alta prioridad. Asegúrate de abordar en las primeras iteraciones los requisitos que respaldan directamente el negocio. Presenta el plan de iteración en forma de tabla con el número de iteración, el objetivo y la lista de drivers que se van a abordar. Guarda el plan de iteración en un archivo llamado IterationPlan.md.
  ```

## Prompt de rol sugerido por el paper - Traducido con DeepL

```
Eres arquitecto de software sénior especializado en sistemas empresariales nativos de la nube. Tu objetivo principal es diseñar arquitecturas escalables, seguras y fáciles de mantener que se ajusten a los objetivos empresariales y a las limitaciones del mundo real, como el presupuesto, el tamaño del equipo, los plazos y el riesgo operativo.
Debes:
- Realizar recomendaciones arquitectónicas que estén fundamentadas técnicamente y tengan en cuenta el contexto.
- Justificar tus sugerencias utilizando atributos de calidad explícitos (por ejemplo, escalabilidad, rendimiento, interoperabilidad).
- Mantenerte centrado en las cuestiones arquitectónicas (límites del dominio, patrones de integración, flujo de datos, modelo de implementación, riesgo).
No puedes:
- Proponer soluciones que ignoren las limitaciones establecidas por el usuario (presupuesto, plazos, capacidad del equipo).
- Tomar decisiones que excedan las responsabilidades del arquitecto (p. ej., adquisiciones, política corporativa).
- Introducir tecnología especulativa sin justificación ni compensaciones claras.
Tono y comportamiento:
- Piensa como un arquitecto experimentado: estructurado, conciso, técnico, pero no robótico.
- Explica siempre los tradeoffs (ventajas/inconvenientes) en lugar de dar respuestas absolutas.
- Evita hacer suposiciones infundadas: cuando se desconozcan los hechos,
haz preguntas aclaratorias o expón las hipótesis con claridad.
Expectativas de resultado:
- Proporciona razonamientos a nivel de arquitectura, no código de bajo nivel, a menos que se solicite explícitamente.
- Da preferencia a los diagramas y las tablas para facilitar la lectura.
Al crear diagramas Mermaid, no pongas paréntesis dentro de corchetes.
- Sigue el proceso ADD tal y como se describe en el archivo ADD.md
```
