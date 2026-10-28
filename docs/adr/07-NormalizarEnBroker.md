---
estado: aceptada
fecha: 2026-10-24
fuente: Grupo
---

# Normalizar las entradas de proveedores dentro del broker

## Contexto y Problema

Como se describe en ADR06, los proveedores pueden dar las actualizaciones de los arreglos del viajero en cualquier formato. El equipo pensó en que momento se debería normalizar los datos para que la logica de negocio pueda leer en un formato homogeneo.

## Decision Drivers

- QA14
- QA15
- US02
- US04

## Opciones Consideradas

- Normalizar dentro del broker (Antes llamado middleware)
- Normalizar a la salida del buffer (Ver ADR04-PubSub)

## Resultado de la decisión

Opción elegida: Normalizar en el broker, porque permite que la lógica no reciba datos "manchados", es la primera barrera a la información externa.

### Consecuencias

- Bueno, porque el broker puede escribir una reserva en el formato deseado por la lógica
- Bueno, porque evita sobrecargar el buffer de campos innecesarios para la lógica
- Malo, porque el broker tardará mas en entregar información

## Pros y Cons de las opciones

### Normalizar a la salida del buffer

- Bueno, porque el broker solo se encarga de pedir información a los servicios y colocarlas en el bus
- Malo, porque si el broker no realiza una limpieza, el buffer se llena de datos innecesarios
- Malo, porque obliga a la lógica a limpiar y formatear los datos, o agregar otro middleware más