---
estado: aceptada
fecha: 2026-10-28
fuente: Grupo
---

# Atacando el rendimiento del sistema en uso normal y picos

## Contexto y Problema

En términos de performance, es necesario garantizar que el servicio se provea de manera equivalente entre usuarios. Esto alcanza a la arquitectura fundamental del sistema y al planeamiento de su deployment.

## Decision Drivers

- QA06
- QA07

## Opciones Consideradas

- Cola de Prioridad
- Load Balancer de usuarios
- Procesamiento secuencial sin colas

## Resultado de la decisión

Hemos elegido aplicar la táctica "Load Balancer" de usuarios porque permite escalar la lógica y repartir las requests de usuario según convenga a cada momento. Aporta resiliencia, admite escalar en ancho y dinamiza el acceso en favor de la performance.

### Confirmación

- Simulando conexiones desde distintos puntos del mundo, cpmprobar que el cliente sea atendido desde distintos servidores.
- Operando en condiciones de estrés del sistema, controlar que no se excedan los límites definidos por las QA06-07:
    - Tiempo de respuesta sostenido (800ms en el 95% de los casos), con 500 solicitudes/seg
    - Mantiene los niveles de rendimiento con 2500 solicitudes/seg

## Pros y Contras de las opciones

### Cola de Prioridad

- Bueno, baja tiempos de respuesta
- Neutral, Introduce intermediarios
- Malo, potencialmente retrasa las escrituras demasiado (starvation)

### Procesamiento secuencial sin colas

- Bueno, Sin capas intermedias
- Bueno, mejor performance en casos generales
- Malo, no permite agregar concurrencia
- Malo, bloqueo de mucho tiempo ante grandes escrituras