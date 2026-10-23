# Architectural Drivers

## Propósito de la ronda de diseño

Para esta primera ronda del proyecto "Trotamundos", el objetivo será producir el diseño que permita construir un prototipo básico. Con este, la startup podrá empezar a analizar la viabilidad del proyecto desde el punto de vista arquitectónico y también desde la perspectiva de mercado.

## Requerimientos Funcionales

**US01 - Panel de Gestión**

Como Viajero quiero ver un panel de gestión (Dashboard) de viajes en línea para ver todas mis reservas existentes.

Criterios de Aceptación:

- Deben estar disponibles todas las reservas activas.
- Las reservas deben estar organizadas por viaje.
- Debe ser accesible a través de un sitio web.
- Debe ser accesible a través de una app para dispositivos móviles.
- Debe mostrar un UI simple centrado en el viaje
- Debe ser el único punto de verdad para los arreglos del viaje (hoteles, autos, vuelos, trenes, autobuses). Combina y muestra datos provenientes de diversas aplicaciones (agencias de viaje, bandeja de correo)
- El viajero debe poder agregar, actualizar y eliminar reservas de la lista manualmente.
- Una vez que el viaje se completa, deben archivarse o eliminarse automáticamente de la vista principal.

**US02 - Detección automática de Reservas**

Como Viajero quiero que mi bandeja de correo electrónico sea escaneada regularmente para agregar automáticamente las reservas al panel.

Criterios de Aceptación:

- Debe conectarse a través de API servida por el proveedor de correo electrónico
- Debe sondear y escanear en busca de correos relacionados con viajes.
- Debe agregar las entradas pertinentes al Dashboard (Ver US01).

**US03 - Filtros y Whitelists**

Como Viajero quiero poder filtrar y crear listas de remitentes seguros para mis reservas de viaje con origen de correo electrónico.

Criterios de Aceptación:

- Las reservas que se añadan al Dashboard con origen de correo electrónico (Ver US02) deben clasificarse con un atributo que especifique su remitente.
- Todas las reservas deben poder agruparse por viaje.
- Cuando el viaje se completa, deben eliminarse de la vista todas las reservas asociadas.
- El Viajero debe poder filtrar las reservas por fecha, destino y remitente.
- El Viajero debe poder crear listas whitelist de remitentes confiables de correo electrónico.

**US04 - Integración con terceros**

Como Viajero quiero que mi dashboard (Ver US01) se mantenga actualizado para mantenerme al tanto de los detalles de reservas, actualizaciones y cancelaciones.

Criterios de Aceptación:

- El sistema debe integrarse con sistemas de viajes e interfaces de agencias de terceros a través de APIs estándar (p/ej. intercambios de aerolíneas o rentadoras).
- La conexión debe ser fluida para la experiencia de usuario.

**US05 - Resolución de Problemas**

Como Viajero quiero poder elegir mi agencia de viajes preferida e integrarla al sistema para facilitar una rápida resolución de problemas

Criterios de Aceptación:

- El sistema debe integrarse con la agencia de viajes preferida del viajero.
- A través de un menú, el viajero debe poder informar una serie de problemas comunes (atención médica, equipaje perdido, vuelo retrasado, etc.)
- "Trotamundos" debe comunicarse con un servicio remoto de la agencia elegida para tratar el problema en cuestión.

**US06 - Analítica de Datos**

Como Miembro del Equipo de Datos quiero tener acceso a registros analíticos para calcular su monetización.

Criterios de Aceptación:

- El Sistema debe recopilar datos analíticos (tendencias, destinos, cancelaciones) de cada reserva.
- Se debe proveer una API de uso interno para acceder a los datos.

**US07 - Compartir reservas**

Como Viajero quiero compartir reservas de mi Dashboard para que personas específicas de mi elección puedan verlas.

Criterios de Aceptación:

- Se debe permitir la creación de itinerarios compartidos (grupos de reservas) en el Dashboard (Ver US01).
- Se deben poder agregar y eliminar reservas a un itinerario compartido.
- Se debe poder eliminar itinerarios compartidos.
- Cada itinerario compartido tiene por defecto un link público para ser compartido.
- Cuando un Viajero que no es el dueño accede al link, se agrega a una lista de pendientes de autorización.
- En todo momento, el Viajero puede Autorizar y Desautorizar a otros a ver sus itinerarios.
- Se debe asegurar que solo personas autorizadas puedan visualizar itinerarios compartidos.
- El sistema debe interoperar con redes sociales para compartir itinerarios.

**US08 - Sistema de Recomendación**

Como Viajero quiero que se me sugieran alternativas de alojamientos/transportes/rutas para conocer nuevas propuestas pensadas para mí.

Criterios de Aceptación:

- En base al análisis del historial y preferencias de los usuarios debe sugerir proactivamente alternativas de alojamiento, transporte o rutas.
- Debe utilizar una optimización human-in-the-loop donde el usuario interactue con la sugerencia, aceptando o ajustando parámetros.
- Debe refinar la recomendación en base a las interacciones del usuario.

## Escenarios de Atributos de Calidad

**QA01 - Performance: Presentar Updates**

Las actualizaciones deben presentarse en la aplicación en menos de 5 minutos desde la generación por la fuente externa.

- Fuente de Estímulo: Sistema externo de proveedores de viajes
- Estímulo: Llega un evento nuevo al itinerario o modificación de uno existente
- Artefacto: Procesamiento y entrega al dashboard del usuario
- Entorno: Operación normal
- Respuesta: La actualización llega, se procesa y se muestra en el dashboard
- Medida de respuesta: La actualización se presenta en menos de 5 minutos desde la generación por la fuente externa en el 95% de los casos

**QA02 - Performance: Tiempo respuesta Web**

El tiempo de respuesta desde la web debe ser de 800ms

- Fuente de Estímulo: Usuario desde la web
- Estímulo: Acciones en la web (consultas, modificaciones)
- Artefacto: Web, backend
- Entorno: Operación normal
- Respuesta: La web recibe la solicitud y responde las acciones del usuario
- Medida de respuesta: El tiempo de respuesta es de 800ms en el 95% de los casos

**QA03 - Performance: Primer contenido mobile**

En plataformas móviles, el primer despliegue de contenido debe ocurrir en menos de 1.4 segundos

- Fuente de Estímulo: Usuario desde plataforma móvil
- Estímulo: Carga la pantalla inicial de la app
- Artefacto: App móvil (pantalla de carga)
- Entorno: Operación normal, red estable
- Respuesta: Muestra el contenido al usuario
- Medida de respuesta: El primer despliegue de contenido ocurre en menos de 1.4 segundos en el 75% de los casos

**QA04 - Availability: Inactividad no planificada**

El sistema debe tolerar un máximo de 5 minutos de inactividad por mes no planificada

- Fuente de Estímulo: Fallo interno de software o hardware
- Estímulo: Una caída no planificada
- Artefacto: Servidor/software/hardware
- Entorno: Durante operación normal
- Respuesta: El sistema detecta el fallo y se recupera adecuadamente
- Medida de respuesta: El tiempo máximo de inactividad no planeada es menor a 5 minutos en un mes con una detección menor a 1 minuto en los incidentes

**QA05 - Scalability: Cantidad cuentas**

La plataforma debe soportar 15 millones de cuentas de usuarios

- Fuente de Estímulo: Usuarios nuevos
- Estímulo: Registro con 15 millones de cuentas almacenadas
- Artefacto: Base de datos
- Entorno: Operación normal con 15 millones de cuentas almacenadas
- Respuesta: La plataforma guarda y soporta el almacenamiento de cuentas de usuario
- Medida de respuesta: Con 15 millones de cuentas, la latencia no degrada fuertemente (300 ms en el 95% de los casos)

**QA06 - Scalability: Actividad semanal**

El sistema debe operar con 2 millones de usuarios semanales activos

- Fuente de Estímulo: 2 millones de usuarios activos
- Estímulo: 500 solicitudes de usuarios por segundo
- Artefacto: Servidor/backend
- Entorno: Operación normal
- Respuesta: El sistema atiende las solicitudes dentro de los tiempos estipulados
- Medida de respuesta: Tiempo de respuesta sostenido (800ms en el 95% de los casos) aun con 500 solicitudes por segundo

**QA07 - Scalability: Picos de trafico**

El sistema debe soportar picos de trafico ante interrupciones importantes de viajes

- Fuente de Estímulo: Ráfaga de usuarios
- Estímulo: Multiples solicitudes en pocos tiempos
- Artefacto: Servidor
- Entorno: Carga maxima
- Respuesta: El servidor responde correctamente a todos los usuarios
- Medida de respuesta: Soporta picos de trafico en ciertos días que superan hasta 5 veces el promedio de uso

**QA08 - Security: Acceso email**

El acceso a los correos debe ser seguro y autorizado

- Fuente de Estímulo: Atacante externo tipo man-in-the-middle
- Estímulo: Intento de capturar datos usando un canal no autorizado
- Artefacto: Comunicación entre nuestro sistema y el proveedor de correo
- Entorno: Operación normal
- Respuesta: Se accede a los datos del correo sin infringir permisos, se cifra el trafico
- Medida de respuesta: 100% de conexiones cifradas, los datos se mantienen seguros de atacantes

**QA09 - Security: Itinerarios compartidos**

Solo las personas específicas por el usuario pueden ver su itinerario

- Fuente de Estímulo: Usuario no autorizado a visualizar un itinerario
- Estímulo: Una persona no autorizada intenta ver el itinerario de un usuario que no lo permitió
- Artefacto: Sistema de autorización de consultas
- Entorno: Operación normal, usuario compartiendo itinerario
- Respuesta: Solo los usuarios permitidos pueden ver el itinerario compartido, se deniega el acceso a cualquier otro
- Medida de respuesta: 0 accesos no autorizados, 100% de accesos autorizados permitidos

**QA10 - Integrability: Nuevos medios de transporte**

Debe permitir una integración fluida de otros medios de transporte en el futuro

- Fuente de Estímulo: Equipo de desarrollo
- Estímulo: Se quiere integrar un nuevo medio de transporte (trenes, buses, etc.)
- Artefacto: API de servicio de transporte, vista en dashboard
- Entorno: Despliegue con el sistema en producción
- Respuesta: El nuevo medio de transporte muestra información desde los servicios de API y visualizarlo en el dashboard
- Medida de respuesta: Menos de 2 minutos de tiempo de inactividad, esfuerzo en desarrollo menor a 10 persona-días

**QA11 - Usability: UI Simple centrada en viaje**

La interfaz debe ser simple, centrada en el viaje, mitigando frustración de rastrear múltiples aplicaciones y correos

- Fuente de Estímulo: Usuario final desde web o app
- Estímulo: Quiere utilizar la aplicación para visualizar su dashboard y realizar consultas de su viaje
- Artefacto: Frontend
- Entorno: Operación normal
- Respuesta: El usuario logra hacer las acciones dentro de la app sin consultar otras fuentes
- Medida de respuesta: Menos de 10 segundos en obtener el dato que quería ver, al menos 90% de tareas hechas sin salir de la app

**QA12 - Usability: Aprovechar capacidades nativas**

El sistema debe aprovechar capacidades nativas (como GPS de móviles) para facilitar las operaciones del usuario

- Fuente de Estímulo: Usuario final en dispositivo móvil
- Estímulo: El usuario inicia una acción que necesita un servicio adicional (como ubicación)
- Artefacto: App móvil, servicios del dispositivo
- Entorno: Operación normal, con permisos ya concedidos
- Respuesta: El sistema logra interactuar con el servicio del dispositivo para obtener el dato necesario
- Medida de respuesta: 90% de datos se obtienen sin consultar al usuario un ingreso manual, se obtiene el dato en menos de 3 segundos

**QA13 - Integrability: Multiregión**

El sistema debe estar preparado arquitectónicamente para operar en diversos países

- Fuente de Estímulo: Responsables del negocio
- Estímulo: Se quiere operar el sistema en otro país
- Artefacto: Sistema, arquitectura, configuración
- Entorno: Tiempo de deploy
- Respuesta: Se agrega el país con sus configuraciones e interactúa con sistemas externos locales
- Medida de respuesta: Esfuerzo menor a 15 persona-días, 0 modificaciones en la lógica central

**QA14 - Interoperability: APIs estándar**

Es imperativa una integración fluida con intercambios de aerolíneas, hoteles y arrendadoras a través de APIs estándar.

- Fuente de Estímulo: Responsables del negocio o del sistema
- Estímulo: Se desea conectar un nuevo servicio de terceros
- Artefacto: Módulo que se conecta con las APIS externas
- Entorno: Operación normal durante intercambio con los servicios
- Respuesta: Respuesta a peticiones HTTP
- Medida de respuesta: Las peticiones son respondidas con status 2xx en el 90% de los casos y pueden parsearse a términos del sistema

**QA15 - Interoperability: Proveedores email**

El sistema debe interoperar con proveedores de correo para el escaneo de mensajes.

- Fuente de Estímulo: Viajero (Usuario)
- Estímulo: Se desea conectar un nuevo servicio de mail
- Artefacto: Módulo que se conecta con las APIS de correo
- Entorno: Operación normal
- Respuesta: Validación del servicio externo, conexión permanente establecida
- Medida de respuesta: El usuario se valida en el servicio externo y queda sincronizado en el 90% de los casos.

**QA16 - Interoperability: Proveedores redes**

El sistema debe interoperar con proveedores de redes sociales para compartir itinerarios.

- Fuente de Estímulo: Viajero (Usuario)
- Estímulo: Se desea conectar una nueva red social
- Artefacto: Módulo que se conecta con las APIS de redes sociales
- Entorno: Operación normal
- Respuesta: Validación del servicio externo, conexión permanente establecida
- Medida de respuesta: El usuario se valida en el servicio externo y queda sincronizado en el 70% de los casos.

## Constraints

C1 - Los viajeros deben usar el sistema desde una web o un dispositivo móvil.

C2 - Se deben registrar decisiones mediante ADRs en formato MADR y utilizar contratos para un diseño y prototipo altamente trazables

## Concerns

- Se deben utilizar tecnologias genericas/interfaces, para no tener dependencias a servicios especificos

## Utility Tree

Formato: (Importancia del negocio, Dificultad técnica)

```Mermaid
---
config:
    treeView:
        rowIndent: 100
        lineThickness: 3
    themeVariables:
        treeView:
            labelFontSize: '18px'
            labelColor: '#7a7b8a'
            lineColor: '#7a7b8a'
---
treeView-beta
title Utility Tree

Utility/
    Performance/
        Latencia
            (H, H) - QA01 "Presentar Updates"
        Responsiveness
            (M, L) - QA02 "Tiempo de Respuesta Web"
            (M, M) - QA03 "Primer contenido Mobile"
    Availability/
        Tolerancia a Fallo
            (H, H) - QA04 "Inactividad no planificada"
    Scalability/
        Carga
            (H, L) - QA05 "Cantidad cuentas"
            (H, M) - QA06 "Actividad semanal"
        Actividad Pico
            (H, H) - QA07 "Picos de tráfico"
    Security/
        Tránsito web
            (H, L) - QA08 "Acceso email"
        Autorización
            (H, M) - QA09 "Itinerarios Compartidos"
    Integrability/
        Funcionalidad Agregada
            (H, L) - QA10 "Nuevos medios de transporte"
        Geográfica
            (H, M) - QA13 "Multiregión"
    Usability/
        User Experience
            (M, L) - QA11 "UI Simple centrada en viaje"
            (L, L) - QA12 "Aprovechar capacidades nativas"
    Interoperability/
        Conexión externa
            (H, M) - QA14 "APIs estándar"
            (H, H) - QA15 "Proveedores email"
            (L, M) - QA16 "Proveedores redes"
```

## Tabla de priorización

Las principales user stories que influencian parte de la arquitectura son:

- US01 (Dashboard) porque es la principal funcionalidad del negocio
- US02 (Detección de emails) porque involucra integración con servicios externos, lectura y sincronización con ellos
- US04 (Integración con terceros) porque involucra integración con servicios externos, soportar uso de APIs con distintos formatos
- ¿ADICIONAL?

Los escenarios fueron priorizados de la siguiente manera:

| Driver                            | Importancia del Negocio | Dificultad Técnica |
| --------------------------------- | ----------------------- | ------------------ |
| QA01 (Presentar updates)          | H                       | H                  |
| QA04 (Inactividad no planificada) | H                       | H                  |
| QA07 (Picos de tráfico)           | H                       | H                  |
| QA15 (Proveedor email)            | H                       | H                  |
| QA06 (Actividad semanal)          | H                       | M                  |
| QA14 (APIs estándar)              | H                       | M                  |
| QA09 (Itinerarios compartidos)    | H                       | M                  |
| QA13 (Multiregion)                | H                       | M                  |
| QA08 (Acceso email)               | H                       | L                  |
| QA05 (Cantidad cuentas)           | H                       | L                  |
| QA10 (Nuevos medios)              | H                       | L                  |
| QA03 (Primer contenido mobile)    | M                       | M                  |
| QA02 (Tiempo respuesta web)       | M                       | L                  |
| QA11 (UI simple)                  | M                       | L                  |
| QA16 (Proveedor redes)            | L                       | M                  |
| QA12 (Capacidades nativas)        | L                       | L                  |
