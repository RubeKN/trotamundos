---
estado: aceptada
fecha: 2026-10-28
fuente: Grupo + LLM
---

# Autorización delegada OAuth 2.0

## Contexto y Problema

El sistema debe leer el correo electronico del viajero para buscar actualizaciones. Esta lectura no debe depender de tener la contraseña del usuario o romper barreras de seguridad

## Decision Drivers

- QA08
- QA15

## Opciones Consideradas

- OAuth 2.0 para gestionar vinculaciones
- Guardar usuario y contraseña del email del viajero

## Resultado de la decisión

Se eligió la opcion de utilizar OAuth 2.0 porque es un estandar no muy complejo de aplicar, nos provee confiabilidad con los clientes de la aplicación y nos despreocupa el acceso seguro.

### Consecuencias

- Bueno, porque nuestro sistema no debe guardar informacion sensible de los usuarios
- Bueno, porque los permisos pueden ser revocados en cualquier momento
- Malo, porque depende que el proveedor este vinculado a este sistema
- Malo, porque los tokens para el acceso pueden caducar

## Pros y Cons de las opciones

### Guardar usuario y contreaseña del email del viajero

- Bueno, porque es simple
- Malo, porque es inviable, la exposición del usuario es maxima. Incumple QA08

## Más información

La decisión fue inicialmente nuestra pero no quedaba claro como se hacía en la iteracion. El LLM le dio forma y nombre a la idea
