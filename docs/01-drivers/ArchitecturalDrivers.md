# Architectural Drivers

## Requerimientos Funcionales


**US01 - Panel de Gestión**  
Como Viajero quiero ver un panel de gestión (Dashboard) de viajes en línea para ver todas mis reservas existentes.  
**Criterios de Aceptación:**
- Deben estar disponibles todas las reservas activas.
- Las reservas deben estar organizadas por viaje.
- Debe ser accesible a través de un sitio web.
- Debe ser accesible a través de una app para dispositivos móviles.
- Debe mostrar un UI simple centrado en el viaje
- Debe ser el único punto de verdad para los arreglos del viaje (hoteles, autos, vuelos, trenes, autobuses). Combina y muestra datos provenientes de diversas aplicaciones (agencias de viaje, bandeja de correo)
- El viajero debe poder agregar, actualizar y eliminar reservas de la lista.


**US02 - Detección automática de Reservas**  
Como Viajero quiero que mi bandeja de correo electrónico sea escaneada regularmente para agregar automáticamente las reservas al panel.  
**Criterios de Aceptación:**
- Debe conectarse a través de API servida por el proveedor de correo electrónico
- Debe sondear y escanear en busca de correos relacionados con viajes.
- Debe agregar las entradas pertinentes al Dashboard (Ver US01).


**US03 - Filtros y Whitelists**  
Como Viajero quiero poder filtrar y crear listas de remitentes seguros para mis reservas de viaje con origen de correo electrónico.  
**Criterios de Aceptación:**
- Las reservas que se añadan al Dashboard con origen de correo electrónico (Ver US02) deben clasificarse con un atributo que especifique su remitente.
- Todas las reservas deben poder agruparse por viaje.
- Cuando el viaje se completa, deben eliminarse de la vista todas las reservas asociadas.
- El Viajero debe poder filtrar las reservas por fecha, destino y remitente.
- El Viajero debe poder crear listas whitelist de remitentes confiables de correo electrónico.


**US04 - Integración con terceros**  
Como Viajero quiero que mi dashboard (Ver US01) se mantenga actualizado para mantenerme al tanto de los detalles de reservas, actualizaciones y cancelaciones.  
**Criterios de Aceptación:**
- El sistema debe integrarse con sistemas de viajes e interfaces de agencias de terceros a través de APIs estándar (p/ej. intercambios de aerolíneas o rentadoras).
- La conexión debe ser fluida para la experiencia de usuario.


**US05 - Resolución de Problemas**  
Como Viajero quiero poder elegir mi agencia de viajes preferida e integrarla al sistema para facilitar una rápida resolución de problemas
**Criterios de Aceptación:**
- El sistema debe integrarse con la agencia de viajes preferida del viajero.
- A través de un menú, el viajero debe poder informar una serie de problemas comunes (atención médica, equipaje perdido, vuelo retrasado, etc.) 
- "Trotamundos" debe comunicarse con un servicio remoto de la agencia elegida para tratar el problema en cuestión.


**US06 - Analítica de Datos**  
Como Miembro del Equipo de Datos quiero tener acceso a registros analíticos para calcular su monetización.  
**Criterios de Aceptación:**
- El Sistema debe recopilar datos analíticos (tendencias, destinos, cancelaciones) de cada reserva.
- Se debe proveer una API de uso interno para acceder a los datos.


**US07 - Compartir reservas:**  
Como Viajero quiero compartir reservas de mi Dashboard para que personas específicas de mi elección puedan verlas.  
**Criterios de Aceptación**
- Se debe permitir la creación de itinerarios compartidos (grupos de reservas) en el Dashboard (Ver US01).
- Se deben poder agregar y eliminar reservas a un itinerario compartido.
- Se debe poder eliminar itinerarios compartidos.
- Cada itinerario compartido tiene por defecto un link público para ser compartido.
- Cuando un Viajero que no es el dueño accede al link, se agrega a una lista de pendientes de autorización.
- En todo momento, el Viajero puede Autorizar y Desautorizar a otros a ver sus itinerarios.
- Se debe asegurar que solo personas autorizadas puedan visualizar itinerarios compartidos.
- El sistema debe interoperar con redes sociales para compartir itinerarios.


**US08 - Req Avanzado (PENDIENTE)**  
Como < rol > quiero < funcionalidad > para < motivo >.  
**Criterios de Aceptación:**
- www


## Escenarios de Atributos de Calidad

## Constraints

## Utility Tree