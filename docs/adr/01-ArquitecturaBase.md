---
estado: aceptada
fecha: 2026-10-28
fuente: Grupo
---

# Elección de una arquitectura general para el sistema

## Contexto y Problema

Como sistema greenfield, lo primero es elegir los cimientos. El equipo planteó propuestas para definir los primeros pasos de diseño.

## Decision Drivers

- Constraint 1 

## Opciones Consideradas

- Cliente-servidor
- Cliente que consulta con terceros

## Resultado de la decisión

Opción elegida: Cliente-servidor porque permite una interacción del usuario con todo el sistema desarrollado, separando lo que es propio del servidor, de la api con la que va a interactuar el cliente.

### Consecuencias

- Bueno, porque tiene toda la logica del negocio centralizada.
- Bueno, porque permite reutilizar las funcionalidades para diferentes clientes.
- Malo, porque puede generar cuello de botella por la centralización de recursos
- Malo, porque esta arquitectura genera un único punto de falla para el sistema completo

### Confirmación

- El cliente-servidor va a permitir la utilización de los servicios desde una web o app movil, y a su vez será el único punto de verdad para realizar arreglos del viaje, descartando la duplicación de datos.

## Pros y Cons de las opciones

### Cliente que consulta con terceros

- Bueno, con un costo menor de construcción del sistema
- Malo, en que no existe una interfaz que unifique los datos para comparar duplicados
