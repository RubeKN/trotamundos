---
estado: aceptada
fecha: 2026-10-24
fuente: Grupo
---

# Uso de Ports & Adapters para la obtención de informacion de terceros

## Contexto y Problema

Los servicios externos tienen la información de los arreglos de los viajeros. Estos envian la información en distintos formatos y se deben solicitar para que la entreguen. En general, el servicio externo no nos va a poder notificar de una actualizacion

## Decision Drivers

- QA15
- QA14
- QA04

## Opciones Consideradas

- Ports & Adapters
- Cliente-Servidor

## Resultado de la decisión

Opción elegida: Ports & Adapters porque permite abstraer al proveedor detras de un puerto, facilitando el cambio de proveedor facilmente.

### Consecuencias

- Bueno, porque permite cambiar los proveedores de terceros facilemtne
- Bueno, porque es un punto central que obtiene los datos de todos los proveedores de terceros
- Neutral, hay que decidir cuando realizar las request a los servicios externos
- Malo, porque implica un codigo más abstracto frente a un cliente-servidor

## Pros y Cons de las opciones

### Cliente-Servidor

- Bueno, porque tiene un flujo de datos claro y una trazabilidad mas sencilla
- Malo, porque requiere que el cliente (El middleware) conozca a quien está consultado
- Malo, si algun proveedor da una funcionalidad asincrona de obtención de información (Mejor performance), no se puede aprovechar

## Más información

Hay que considerar un tiempo claro de sondeo en intervalos cortos para asegurar los 5 minutos de tope. Podrian ser 2 minutos como maximo.
