---
estado: "{propuesta | rechazada | aceptada | obsoleta | reemplazada por ADR-0123}"
fecha: { YYYY-MM-DD de la ultima actualización }
fuente: { Grupo | LLM }
---

# Uso de Cola de mensajes P2P para la integración asíncrona

## Contexto y Problema

Al refinar el módulo de Integraciones Externas (Iteración 2), se identificó la necesidad de definir cómo se entregará la información obtenida de los proveedores de terceros hacia la lógica central del sistema. Es necesario asegurar que la presentación de actualizaciones en el dashboard sea fluida y que el sistema tolere fallos sin afectar la experiencia de usuario.


## Decision Drivers

- QA01 
- QA04
- US01 

## Opciones Consideradas

- Cola de mensajes punto a punto
- Publisher-Subscriber
- Pipes and filters

## Resultado de la decisión

Opción elegida: Cola de mensajes punto a punto, porque permite procesar las actualizaciones de los sistemas externos de forma asíncrona, desacoplando completamente al productor (el middleware de integraciones) del consumidor (la lógica central). Se eligió en vez de Pub-Sub, ya que en nuestro contexto el consumidor de los datos será únicamente el propio sistema, haciendo innecesaria la complejidad de multiples consumidores.

### Consecuencias

- Bueno, porque el asincronismo permite una mejor disponibilidad en el dashboard y tiempos de respuesta más rápidos.
- Bueno, porque desacopla al publicador y al receptor, aportando tolerancia a fallos (si la lógica central se cae, los mensajes quedan en la cola).
- Malo, porque incrementa la complejidad operativa agregando un componente adicional a la infraestructura
- Malo, porque introduce consistencia eventual en el sistema (los datos pueden tardar en verse reflejados en el Dashboard).

### Confirmación

Para confirmar el correcto cumplimiento de este ADR, se debera verificar en el momento de despliegue y flujo de datos: 
- Puerto Unico de Proveedores por el cual se colocan los datos formateados en la Cola de Mensajes.
- Modulo de "Arreglos de viaje" debe consumir los datos asincronamente, sin que exista invocación directa entre ambos módulos.

## Pros y Cons de las opciones

### Pub-Sub

- Bueno, porque garantiza un bajo acoplamiento y permite notificar a varios consumidores.
- Malo, porque al tener un solo consumidor no logra ningún valor real y agrega complejidad innecesaria.
- Malo, implica una causa de consistencia eventual y el buffer se puede volver un punto único de falla.

### Pipes and Filters

- Bueno, porque es muy modificable y permite alta reutilización con un acoplamiento bajo.
- Malo, porque tiene bajo rendimiento debido al overhead de latencia entre filtros.
- Malo, porque degrada la interactividad con el usuario, perjudicando a la performance (QA01).
