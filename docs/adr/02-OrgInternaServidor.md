---
estado: aceptado
fecha: 2026-10-28
fuente: Grupo
---

# La elección (ADR01) de una arquitectura causa alta centralidad

## Contexto y Problema

Al definir (ADR01) una arquitectura general de Cliente-Servidor, corresponde ahora definir la lógica interna del server en términos de arquitectura. El equipo plantea alternativas considerando los drivers.

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
