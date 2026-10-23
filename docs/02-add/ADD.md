# ADD - Attribute Driven Design

## Descripción del método ADD
El objetivo principal del método ADD es guiar el proceso de diseño satisfaciendo los architectural drivers del sistema.
El diseño de la arquitectura se realiza en rounds, cada una con una serie de iteraciones. Al final de una round, luego de varias iteraciones, se produce una arquitectura que encaja con el proposito de la ronda.
En cada iteración se realizan una serie de pasos. Los pasos 1-7 involucran un round, los pasos 2-7 se iteran varias veces dentro del round

### Step 1: Review inputs
Confirmar que se cuenta con la información necesaria y los drivers claros, completos y priorizados. Esto incluye, proposito del round de diseño, requerimientos funcionales claros, escenarios de atributos de calidad con sus 6 pasos completos, constraints y concerns. Estos drivers deben ser priorizados antes de empezar

### Step 2: Establish Iteration Goal by Selecting Drivers
Cada iteración se centra en cumplir una meta particular. La meta implica diseñar para satisfacer un subconjunto de los drivers que ya fueron priorizados y puestos en el backlog de la arquitectura.
Debes registrar la meta de la iteración y que drivers fueron seleccionados

### Step 3: Choose One or More Elements of the System to Refine
Para satisfacer drivers se deben tomar decisiones, que se manifiestan en estructuras de la arquitectura compuestas de elementos/modulos/componentes interrelacionados.
Para un sistema greenfield, el unico elemento disponible es el sistema en si que se debe refinar.
Para un sistema groundfield o donde ya se han tomado decisiones previas, los elementos suelen ser los resultados de iteraciones anteriores y pueden ser descompuestos en elementos mas finos (top-down approach) o combinandolos en elementos mas grandes (bottom-up approach)

### Step 4:Choose One or More Design Concepts That Satisfy the Selected Drivers
En este paso, se eligen conceptos de diseños para cumplir la meta de la iteración. Los conceptos de diseños incluyen:
- Patrones de diseño: Soluciones generales a cuestiones especificas a nivel de código
- Estilos arquitectónicos: Paquete de decisiones ya tomadas, con su vocabulario, topología, restricciones, ventajas y desventajas. Pueden ser estilos unicos, o combinación overlay o jerárquica
- Tácticas arquitectónicas: Estrategias probadas que apuntan a un atributo de calidad particular
- Arquitectura de referencias: Mapping de un conjunto de funcionalidades en elementos de software e interfaces
- Componentes externos previamente desarrollados: Incluye frameworks o recursos cloud especificos

Registrar las decisiones en una tabla indicando, que concepto de diseño se selecciona, cuales alternativas se descartan y una justificación.

### Step 5: Instantiate Architectural Elements, Allocate Responsibilities, and Define Interfaces
Los elementos elegidos son adaptados para abordar los drivers que componen la meta de la iteración. Esto puede llevar a crear nuevos elementos o modificar los existentes.
Despues de instanciar los elementos se deben asignar responsabilidades a ellos y luego definir las interfaces para poder conectarse y colaborar con otros elementos
Se debe justificar la instanciacion, asignacion de responsabilidades y definicion de interfaces elegida.

### Step 6: Sketch Views and Record Design Decisions
Capturar el resultado de la arquitectura representando las estructuras mediante diagramas y documentando las decisiones mediante MADR.
Crear un nuevo diagrama en el documento de la arquitectura para visualizar la decision.

### Step 7: Perform Analysis of Current Design and Review Iteration Goal and Achievement of Design Purpose
Se deben analizar las decisiones tomadas, individualmente y como conjunto para evaluar si satisfacen los drivers fijados en la meta de la iteración. Responder: ¿Cuanto diseño llevamos hecho? ¿Se cumplió el objetivo? ¿Hace falta otra iteración?, si todavia hay drivers prioritarios sin abordar o incertidumbre, se debe iterar repitiendo desde el paso 2.