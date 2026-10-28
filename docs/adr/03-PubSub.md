---
estado: reemplazada por ADR05
fecha: 2026-10-24
fuente: Grupo
---

# Elección de herramienta asíncrona para presentación de actualizaciones

## Contexto y Problema

Atacando QAs de performance y availability. A nivel estructural, vemos que es urgente definir estilos arquitectónicos que permitan una rápida actualización del Dashboard ante la llegada de nuevos datos por parte de servicios externos. Asimismo, es importante asegurar que el sistema sea tolerante a fallos.

## Decision Drivers

- QA01
- QA04

## Opciones Consideradas

- Estilo arquitectónico Publisher-Subscriber
- Estilo arquitectónico Cliente-Servidor
- Estilo arquitectónico Ports & Adapters

## Resultado de la decisión

Opción elegida: Estilo arquitectónico Publisher-Subscriber, porque es la opción que mejor cumple el criterio determinante para la decisión (Optimizar el sistema en performance y availability)

### Consecuencias

- Afecta positivamente independizando la lectura de nuevos datos respecto de las tecnologías productoras
- Afecta positivamente añadiendo asincronía al proceso de integrar nuevas reservas. Esto permite que el sistema se recupere rápido ante la caída de un proveedor de servicio (o su conexión).
- Agrega un factor de centralidad respecto del buffer. Puede afectar negativamente por ser rigido, además el sistema entero depende de ese módulo en todo momento.

### Confirmación

Para confirmar el correcto cumplimiento de este ADR, debe verificarse que la lógica de Trotamundos consume datos de forma asincrona de los servicios externos a través de sus publishers. Además debe verificarse que dicho consumo sea unidireccional (no hay forma de comunicarse con el exterior).

## Pros y Cons de las opciones no elegidas

### Cliente-Servidor

- Malo por ser propicio a debilitar el sistema constituyendo un único punto de falla. Va en contra de QA04
- Mejoraría en reusabilidad de servicios

### Ports & Adapters

- Bueno para otra parte del sistema.

## Más información
La decisión surgió en base a brainstorming y debate del equipo entero, contando con concenso total. Posteriormente fue validada por las decisiones del LLM en la misma iteración.