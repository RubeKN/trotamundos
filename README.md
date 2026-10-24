# trotamundos

## Objetivo del proyecto
Inicialmente, el grupo pensó en seguir las recomendaciones del paper "Better Together" para hacer un diseño colaborativo humano/LLM. La captura de drivers y su revisión (Paso 1 ADD) fue principalmente hecha por el grupo y, al momento de generar el archivo Architecture.md, como sugiere el paper, nos resulta difícil juzgar la validez de lo producido por el LLM. Por falta de experiencia en construcción de proyectos reales del grupo, caeríamos en el sesgo muy fácilmente.

En base a esto, decidimos hacer en primera instancia las iteraciones de ADD a mano (`/docs/02-add/iteracion-n.md`). Posteriormente, se simula la iteración por medio del LLM siguiendo las recomendaciones y prompts del paper "Better Together" (`/docs/02-add/iteracion-n-llm.md`). Finalmente, estas se contrastan y ponderan, dando como resultado un conjunto de decisiones. Las mismas se documentan en formato MADR en la carpeta `/docs/adr/`.

## Escenarios de atributos de calidad
- Se aprovechó la construccion previa de la [skill](https://github.com/Dalviux9th/wonderful-skill) para escenarios de qa para orientar el diseño de escenarios
- Los parametros de medida de respuestas fueron consultados al LLM con la skill asumiendo un equipo de startup que busca bajo costos y una implementacion rapida