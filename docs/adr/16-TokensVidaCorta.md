---
estado: aceptada
fecha: 2026-10-28
fuente: LLM
---

# Tokens de vida corta para autenticar viajeros

## Contexto y Problema

Con el monolito en varias instancias repartidas con el load balancer (ADR08) la identificacion de viajeros debe ser sencilla para evitar atarlo a una instancia.

## Decision Drivers

- QA09
- QA04
- QA06
- QA07

## Opciones Consideradas

- Tokens de acceso de vida corta + token de refresco
- Sesión en memoria
- Sesión en base de datos compartida

## Resultado de la decisión

Opción elegida: Tokens de acceso de vida corta + refresco, ya que permite que la firma se realice en la instancia al que se asigna al usuario

### Consecuencias

- Bueno, porque cualquier instancia puede validar sin revisar un estado compartido
- Bueno, porque escala junto con el balanceo
- Malo, porque la revoación inmediata no es posible, solo puede expirar
- Malo, porque la rotación de claves exige gestión
- Neutral, el uso de un access token de vida corta requiere revocación del refesh token en el servicio de identidad

## Pros y Cons de las opciones

### Sesión en memoria

- Bueno, simple de implementar
- Malo, si se cae la instancia el viajero pierde la sesión

### Sesión en base de datos compartida

- Bueno, la revocación inmediata es posible
- Malo, porque la base de datos compartida es un componente critico
- Malo, cada request de cualquier instancia ataca la misma base de datos
