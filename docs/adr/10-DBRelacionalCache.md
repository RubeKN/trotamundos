---
estado: aceptada
fecha: 2026-10-27
fuente: Grupo
---

# DB Relacional y Caché para consultas frecuentes

## Contexto y Problema

Atacando QAs de escalabilidad. Hay que persistir 15 millones de cuentas y atender lecturas y escrituras del Dashboard. Las lecturas son más frecuentes que las escrituras, así que no conviene ir a la base en cada consulta. El alcance es la capa de datos de las operaciones del usuario (primaria, réplicas y caché).

## Decision Drivers

- QA05
- QA06
- QA07

## Opciones Consideradas

- Base de Datos Relacional + Caché
- Base de Datos NoSQL

## Resultado de la decisión

Opción elegida: Base de Datos Relacional + Caché, porque aprovecha la simplicidad del modelo de datos frente a NoSQL y, con la caché, soporta las lecturas masivas del Dashboard.

### Consecuencias

- Bueno, porque el modelo relacional es simple y de uso general para el equipo.
- Bueno, porque la caché guarda consultas frecuentes y evita acceder a la base en cada lectura.
- Bueno, porque las escrituras van a una base primaria que mantiene consistentes las réplicas (sobreescribiendo) y la caché (invalidando).
- Malo, porque hay costo en replicación y almacenamiento de grandes volúmenes de datos.

### Confirmación

Para confirmar el correcto cumplimiento de este ADR, debe verificarse que las lecturas van primero a la caché y, si no está el dato, a una réplica. Las escrituras deben ir a la primaria, replicarse e invalidar la caché de los datos cambiados.

## Pros y Cons de las opciones no elegidas

### Base de Datos NoSQL

- Bueno, porque el modelo basado en documentos escala horizontalmente con facilidad para el volumen de usuarios proyectado y permite servir las vistas principales sin operaciones complejas de relación.
- Malo, porque las entidades principales del sistema están fuertemente interrelacionadas y compartidas.En NoSQL esto obliga a desnormalizar y duplicar información, o a resolver las relaciones manualmente.
- Malo, porque implicaria una curva de aprendizaje mayor para el equipo

## Más información

La decisión surgió en base a brainstorming y debate del equipo entero, contando con concenso total. El LLM coincidió en usar caché de lectura e invalidarla al escribir. 
