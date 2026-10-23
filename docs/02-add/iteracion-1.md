# Iteración 1 - Descomponiendo "Trotamundos"

## PASO 2 - Objetivo de la Iteración
Descomponer el sistema Trotamundos en sí mismo. Definir Aspectos básicos de la arquitectra como estilo arquitectónico general.

**Drivers a desarrollar en la iteración:**
US01 - Dashboard
QA01 - Presentar actualizaciones
QA04 - Inactividad no planificada
QA14 - APIs estándar
QA15 - Proveedor email


## PASO 3 - Descomposición
Como estamos diseñando un sistema greenfield, el elemento a descomponer es el sistema entero.


## PASO 4 - Aplicando conceptos de diseño a los drivers seleccionados
**Alternativas propuestas:**

| Alternativa        | Pros                                                               | Contras                                                         | Drivers relacionados |
|--------------------|--------------------------------------------------------------------|-----------------------------------------------------------------|----------------------|
| Ports and Adapters | Independencia de la tecnología, modificabilidad, interoperabilidad | Complejidad de diseño (Muchas abstracciones e indirecciones)    | QA14, QA15           |
| Cliente-Servidor   | Lógica centralizada, reusabilidad de servicios                     | Cuello de Botella, único punto de falla                         | QA04 (Negativo)      |
| Pub-Sub            | Bajo acoplamiento, interoperabilidad, disponibilidad               | Perdida de consistencia, Baja trazabilidad, no admite sincronía | QA01, QA04           |

Al atacarse los QA14 y QA15 con _"Ports & Adapters"_ y los QA01 y QA04 con _"Pub-Sub"_, se puede plantear una combinación de estilos de tipo **overlay**.


## PASO 5 - Instanciar elementos, asignar responsabilidades y definir interfaces
La lógica del sistema (aún pendiente de refinamiento) actúa como **subscriber** de un canal atendido por un middleware (**publisher**). Este mismo es el core de un módulo "ports and adapters" el cual tendrá las interfaces (**puertos**) para comunicarse con los diferentes servicios externos (**adapters**), como proveedores de email, agencias de viaje, vuelos, etc.

ports and adapters se encarga de conectar con los servicios externos de forma síncrona (lanzando peticiones en un intervalo fijo de tiempo). Además, formatea cada entrada al estilo del subscriber y las publica en un buffer de actualizaciones. Dicho subscriber contiene toda la lógica restante (Se refinará más adelante).


## PASO 6 - Vistas

PENDIENTE: Digitalizar vistas en papel

## PASO 7 - Revisar la aplicación del método

Como primera iteración en un sistema greenfield, tomamos una user story de referencia (US01) buscando entender el sistema mismo mientras se diseña. La misma no fue atacada directamente, sino como fuente de contexto para la toma de decisiones que definan la estructura base de la arquitectura. En cuanto a avances concretos, se descompuso el módulo más crítico de la arquitectura en términos de Performance, disponibilidad e interoperabilidad con terceros.

En esta iteración se ve claramente (fig. 1.2) que resulta imperativo el desarrollo del módulo subscriber (lógica del negocio). Ahí se encuentra la mayor cantidad de incertidumbre del sistema. Además, la elección de Pub-Sub delega la conexión externa al publisher, liberándonos de esta carga para centrarnos en la lógica restante.