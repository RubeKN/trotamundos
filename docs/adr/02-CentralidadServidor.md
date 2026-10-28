---
estado: reemplazada por ADR09
fecha: 2026-10-28
fuente: Grupo
---

# La elección (ADR01) de una arquitectura causa alta centralidad

## Contexto y Problema
Como equipo es un concern que la elección de una arquitectura centralizada cause degradación de la performance o accesibilidad del sistema. En futuras iteraciones, se buscará investigar el riesgo e impacto de esto. Eventualmente se plantearán soluciones paleativas.

## Decision Drivers

- US01
- QA13

## Opciones Consideradas

- Monolito modular
- Microservicios

## Resultado de la decisión

Opción elegida: Monolito modular, ya que este permite ver al servidor como una unica unidad, pero que dentro las funciones tienen una separación bien definida. En un futuro, en caso de ser necesario, se podría migrar a microservicios pero generaría complejidad de implementación de cambios.

### Consecuencias

- Bueno, porque obtenemos un despliegue único
- Bueno, porque es fácil de operar con los modulos
- Bueno, porque los límites entre módulos estan bien definidos
- Malo, porque escalar horizontalmente implica una réplica del servidor

### Confirmación

- Tener un monolito modular nos va a permitir separar las funcionalidades dentro del mismo sistema de manera segura y simple. 

## Pros y Cons de las opciones

### Microservicios

- Bueno, ya que hay un escalado y despliegue independiente por servicio
- Malo, porque tiene un alto costo operativo.
