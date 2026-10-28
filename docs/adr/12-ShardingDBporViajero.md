---
estado: aceptada
fecha: 2026-10-27
fuente: LLM
---

# Dividir los datos (sharding) por idViajero

## Contexto y Problema

En el ADR07 se planteó agregar una caché para las lecturas, pero esto no soluciona el problema de picos de trafico, ya que la caché se puede saturar. Se debe proveer un mecanismo para soportar la alta cantidad de usuario. Se pensó como 15 millones de personas como 15 millones de registros, pero este número estará multiplicado por N arreglos de viajes de cada usuario.

## Decision Drivers

- QA05
- QA06
- QA07

## Opciones Consideradas

- Sharding con separación por idViajero
- Única base de datos

## Resultado de la decisión

Opción elegida: Sharding con separación por idViajero, al separar por idViajero las consultas de un usuario se piden dentro de la misma partición. Además de permitir separar la carga.

### Consecuencias

- Bueno, porque no sobrecarga una única base de datos de lectura
- Bueno, porque los usuarios solo requiere consultar un nodo para ver sus viajes en el dashboard
- Malo, porque requiere mas complejidad en arquitectura

### Confirmación

Se puede probar una concurrencia masiva automatica (con Hurl, por ejemplo) para verificar que la latencia no se degrada altamente

## Pros y Cons de las opciones

### Única base de datos

- Bueno, porque es mas simple de implementar bajo el modelo relacional
- Malo, porque ante un pico de trafico, la caché fallará constantemente degradando la latencia
- Malo, porque una unica base con gran cantidad de registros un disco con mayor almacenamiento (mas costos)
