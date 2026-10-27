---
estado: Aceptada
fecha: 27/10/2026
---

# Tratamiento de consultas y escrituras

## Contexto y Problema

Ante la alta demanda de solicitudes de los usuarios, el sistema debe ser capaz de operar con normalidad, permitiendo un promedio de uso de 2 millones de usuarios activos semanales. Como sabemos que hay más lecturas que escrituras, hay que priorizar la solución rápida de ellas, por lo que habría que implementar una estrategia para tener en cuenta estos casos.

## Decision Drivers

QA06-Scalability: Actividad semanal

## Opciones Consideradas

- Cola de prioridad
- Procesamiento secuencial sin colas

## Resultado de la decisión

Elegimos la opción de cola de prioridad, ya que es una alternativa que mejora el tiempo de respuesta de consultas, permitiendo utilizar concurrencias para casos de alta demanda de consultas. Consideramos que generalmente van a ocurrir más consultas que escrituras, por lo que vamos a tomar eso como prioritario.

### Consecuencias

Pros: Mejores tiempos de respuesta ante consultas al dashboard.
Contras: Introduce intermediarios, puede retrasar las escrituras demasiado (starvation).

### Confirmación

Ante muchas requests de los usuarios, se priorizara consultas sobre escrituras, y en caso de que todas las solicitudes sean del mismo tipo, se priorizara las solicitudes por orden de llegada.

## Pros y Cons de las opciones

### Procesamiento secuencial sin colas

- Pros: No utiliza capas intermedias, por lo que mejora la performance en los casos generales, tanto de lectura como escritura.

- Contras: No permite agregar concurrencia y también bloquea el sistema por mucho tiempo si se requiere una gran escritura.
