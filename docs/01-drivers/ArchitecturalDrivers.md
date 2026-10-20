# Architectural Drivers

## Requerimientos Funcionales

## Escenarios de Atributos de Calidad
QA01 - Performance: Las actualizaciones deben presentarse en la aplicación en menos de 5 minutos desde la generación por la fuente externa.
* Fuente de Estímulo: Sistema externo de proveedores de viajes
* Estímulo: Llega un evento nuevo al itinerario o modificación de uno existente
* Artefacto: Procesamiento y entrega al dashboard del usuario
* Entorno: Operación normal
* Respuesta: La actualización llega, se procesa y se muestra en el dashboard
* Medida de respuesta: La actualización se presenta en menos de 5 minutos desde la generación por la fuente externa en el 95% de los casos

QA02 - Performance: El tiempo de respuesta desde la web debe ser de 800ms
* Fuente de Estímulo: Usuario desde la web
* Estímulo: Acciones en la web (consultas, modificaciones)
* Artefacto: Web, backend
* Entorno: Operación normal
* Respuesta: La web recibe la solicitud y responde las acciones del usuario
* Medida de respuesta: El tiempo de respuesta es de 800ms en el 95% de los casos

QA03 - Performance: En plataformas móviles, el primer despliegue de contenido debe ocurrir en menos de 1.4 segundos
* Fuente de Estímulo: Usuario desde plataforma móvil
* Estímulo: Carga la pantalla inicial de la app
* Artefacto: App móvil (pantalla de carga)
* Entorno: Operación normal, red estable
* Respuesta: Muestra el contenido al usuario
* Medida de respuesta: El primer despliegue de contenido ocurre en menos de 1.4 segundos en el 75% de los casos

QA04 - Availability: El sistema debe tolerar un máximo de 5 minutos de inactividad por mes no planificada
* Fuente de Estímulo: Fallo interno de software o hardware
* Estímulo: Una caída no planificada
* Artefacto: Servidor/software/hardware
* Entorno: Durante operación normal
* Respuesta: El sistema detecta el fallo y se recupera adecuadamente
* Medida de respuesta: El tiempo máximo de inactividad no planeada es menor a 5 minutos en un mes con una detección menor a 1 minuto en los incidentes

QA5 - Scalability: La plataforma debe soportar 15 millones de cuentas de usuarios
* Fuente de Estímulo: Usuarios nuevos
* Estímulo: Registro con 15 millones de cuentas almacenadas
* Artefacto: Base de datos
* Entorno: Operación normal con 15 millones de cuentas almacenadas
* Respuesta: La plataforma guarda y soporta el almacenamiento de cuentas de usuario
* Medida de respuesta: Con 15 millones de cuentas, la latencia no degrada fuertemente (300 ms en el 95% de los casos)

QA06 - Scalability: El sistema debe operar con 2 millones de usuarios semanales activos
* Fuente de Estímulo: 2 millones de usuarios activos
* Estímulo: 500 solicitudes de usuarios por segundo
* Artefacto: Servidor/backend
* Entorno: Operación normal
* Respuesta: El sistema atiende las solicitudes dentro de los tiempos estipulados
* Medida de respuesta: Tiempo de respuesta sostenido (800ms en el 95% de los casos) aun con 500 solicitudes por segundo

QA07 - Scalability: El sistema debe soportar picos de trafico ante interrupciones importantes de viajes
* Fuente de Estímulo: Rafaga de usuarios
* Estímulo: Multiples solicitudes en pocos tiempos
* Artefacto: Servidor
* Entorno: Carga maxima
* Respuesta: El servidor responde correctamente a todos los usuarios
* Medida de respuesta: Soporta picos de trafico en ciertos días que superan hasta 5 veces el promedio de uso

QA08 - Security: El acceso a los correos debe ser seguro y autorizado
* Fuente de Estímulo: Atacante externo tipo man-in-the-middle
* Estímulo: Intento de capturar datos usando un canal no autorizado
* Artefacto: Comunicación entre nuestro sistema y el proveedor de correo
* Entorno: Operación normal
* Respuesta: Se accede a los datos del correo sin infringir permisos, se cifra el trafico
* Medida de respuesta: 100% de conexiones cifradas, los datos se mantienen seguros de atacantes

QA09 - Security: Solo las personas específicas por el usuario pueden ver su itinerario
* Fuente de Estímulo: Usuario no autorizado a visualizar un itinerario
* Estímulo: Una persona no autorizada intenta ver el itinerario de un usuario que no lo permitió
* Artefacto: Sistema de autorización de consultas
* Entorno: Operación normal, usuario compartiendo itinerario
* Respuesta: Solo los usuarios permitidos pueden ver el itinerario compartido, se deniega el acceso a cualquier otro
* Medida de respuesta: 0 accesos no autorizados, 100% de accesos autorizados permitidos

QA10 - Integrability: Debe permitir una integración fluida de otros medios de transporte en el futuro
* Fuente de Estímulo: Equipo de desarrollo
* Estímulo: Se quiere integrar un nuevo medio de transporte (trenes, buses, etc.)
* Artefacto: API de servicio de transporte, vista en dashboard
* Entorno: Despliegue con el sistema en producción
* Respuesta: El nuevo medio de transporte muestra información desde los servicios de API y visualizarlo en el dashboard
* Medida de respuesta: Menos de 2 minutos de tiempo de inactividad corto, esfuerzo en desarrollo menor a 10 persona-días

QA11 - Maintainability: Se deben registrar decisiones mediante ADRs en formato MADR y utilizar contratos para un diseño y prototipo altamente trazables
* Fuente de Estímulo: Arquitectos de software
* Estímulo: Nueva decisión de diseño
* Artefacto: Documentación del proyecto
* Entorno: Tiempo de desarrollo, antes del despliegue
* Respuesta: Los ADR son legibles, siguen el formato MADR y son útiles para el diseño e implementación del prototipo
* Medida de respuesta: El diseño y prototipo se pueden trazar claramente con los ADRs documentados

QA12 - Usability: La interfaz debe ser simple, centrada en el viaje, mitigando frustración de rastrear múltiples aplicaciones y correos
* Fuente de Estímulo: Usuario final desde web o app
* Estímulo: Quiere utilizar la aplicación para visualizar su dashboard y realizar consultas de su viaje
* Artefacto: Frontend
* Entorno: Operación normal
* Respuesta: El usuario logra hacer las acciones dentro de la app sin consultar otras fuentes
* Medida de respuesta: Menos de 10 segundos en obtener el dato que quería ver, al menos 90% de tareas hechas sin salir de la app

QA13 - Usability: El sistema debe aprovechar capacidades nativas (como GPS de móviles) para facilitar las operaciones del usuario
* Fuente de Estímulo: Usuario final en dispostivo móvil
* Estímulo: El usuario inicia una acción que necesita un servicio adicional (como ubicación)
* Artefacto: App móvil, servicios del dispositivo
* Entorno: Operación normal, con permisos ya concedidos
* Respuesta: El sistema logra interactuar con el servicio del dispositivo para obtener el dato necesario
* Medida de respuesta: 90% de datos se obtienen sin consultar al usuario un ingreso manual, se obtiene el dato en menos de 3 segundos

QA14 - Integrability: El sistema debe estar preparado arquitectónicamente para operar en diversos paises
* Fuente de Estímulo: Responsables del negocio
* Estímulo: Se quiere operar el sistema en otro país
* Artefacto: Sistema, arquitectura, configuracion
* Entorno: Tiempo de deploy
* Respuesta: Se agrega el país con sus configuraciones e interactúa con sistemas externos locales
* Medida de respuesta: Esfuerzo menor a 15 persona-días, 0 modificaciones en la lógica central

## Constraints
C1 - Los viajeros deben usar el sistema desde una web o un dispositivo móvil

C2 - Debe interoperar con sistemas de viajes y agencias de terceros a traves de APIs estandar

C3 - Debe interoperar con proveedores de correo para escanear mensajes

## Utility Tree

## PREGUNTAR

Considero que el tema de APIs y correo es una restriccion, pero en el enunciado aparece como QA de interoperabilidad