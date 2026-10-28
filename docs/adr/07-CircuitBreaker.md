---
estado: aceptada
fecha: 2026-10-24
fuente: LLM
---

# Circuit breaker por preveedor con reintentos acotados

## Contexto y Problema

Un proveedor caido no debe degradar el sistema si se cae ni sobrecargar el broker causando degradación en la lectura de otros proveedores. El usuario debe ser avisado si un proveedor no está funcionando correctamente

## Decision Drivers

- QA04
- QA14

## Opciones Consideradas

- Circuit breaker con reintentos acotados
- Reintentar sin limite
- Fallar y propogar el error

## Resultado de la decisión

Opción elegida: Circuit breaker con reintentos acotados y retry con tiempos cada vez mas progresivos porque permite negar temporalmente un servicio ante multiples fallas, sin negarlo por completo ante la primera falla

### Consecuencias

- Bueno, porque el fallo queda contenido sin llegar al cliente
- Bueno, porque ante N numero de retries se puede detener la consulta, dar aviso al usuario e intentar devuelta en un tiempo mas largo.
- Neutral, hay que revisar los umbrales correctos para no negar un servicio ante una solución rápida

## Pros y Cons de las opciones

### Reintentar sin limite

- Malo, entra en un wait infinito gastando recursos haciendo solicitudes
- Malo, nunca informa al usuario la razón que no llegan las actualizaciones del proveedor caido

### Fallar y propagar el error

- Malo, porque no cumple la QA04