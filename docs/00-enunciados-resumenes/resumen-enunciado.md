# Resummen enunciado
## Objetivos y entrega
Identificar, capturar y documentar las decisiones de diseño.
Construir la arquitectura de software.
Metodo ADD (Attribute-Driven Design)
Implementar un prototipo que demuestre la viabilidad de la arquitectura propuesta.

Antes de iniciar el metodo ADD se debe hacer un analisis detallado de los requerimientos e identificar el alcance del sistema a diseñar.
Elaborar un diagrama de contexto (Limites del sistema e interacciones con actores externos)
Priorizar requerimientos funcionales y atributos de calidad

Capturar iteraciones del proceso y artefactos resultantes (intermedios y finales) en un repo de Github.
4 iteraciones de ADD (minimo)
Capturar decisiones de diseño usando ADRs bajo el formato MADR
Crear vistas arquitectonicas adecuadas que reflejen las estructuras del sistema
Enfoque Spec-driven development tanto para el diseño como la implementación

Claridad precision y completitud en la documentacion entregada (ADD, vistas, ADRs), uso correcto de patrones y tacticas de diseño. Codigo del propotipo trazable y consistente con la arquitectura documentada.

## SISTEMA "TROTAMUNDOS"
Una startup quiere construir un panel de gestion de viajes en linea.
Permitir que los viajeros vean sus reservas existenes organizadas por viaje
Unico punto de verdad para todos los arreglos del viaje (hoteles, autos, vuelos, tenes, autobuses)
Desde la web o dispositivo movil
Interfaz simple centrada en el viaje, mitigando el uso de multiples aplicaciones y bandejas de correo
Soportar carga de 2 millones de usuarios activos por semana
15 millones de cuentas de usuario
Picos de uso entre domingo-lunes, jueves-viernes, y durante interrupciones importantes de viajes (como problemas climaticos)

### Requerimientos funcionales principales
- Procesamiento de Correo: El sistema debe sondear y escanear el correo electrónico de los usuarios en busca de correos relacionados con viajes para agregar automáticamente las reservas al itinerario.
- Filtros y Whitelists: Debe permitir filtrar y crear listas de remitentes seguros (whitelists) para ciertos correos electrónicos de viaje.
- Integración con Terceros: El sistema debe integrarse de manera fluida con sistemas de viajes e interfaces de agencias de terceros a través de APIs estándar (por ejemplo, intercambios de aerolíneas o rentadoras) para obtener detalles de las reservas, actualizaciones y cancelaciones.
- Gestión Manual: Los clientes deben poder agregar, actualizar o eliminar sus reservas existentes de forma manual dentro del panel.
- Ciclo de Vida del Viaje: Los elementos en el panel de control deben poder agruparse por viaje, y una vez que el viaje se completa, deben archivarse o eliminarse automáticamente de la vista principal.
- Resolución de Problemas: El sistema debe integrarse con la agencia de viajes preferida del usuario para facilitar una rápida resolución de problemas.
- Analítica de Datos: "Trotamundos" recopilará datos analíticos de los viajes (tendencias, destinos,
cancelaciones) para su monetización por parte del equipo de datos, implicando la ejecución de consultas analíticas pesadas.

### Requerimientos funcionales secundarios (Segunda entrega)
Elegir e incorporar al menos uno de los siguientes
- Opción A, Sistema de Recomendación: Incorporar un módulo que aplique técnicas de análisis sobre el historial y preferencias de los usuarios para sugerir proactivamente alternativas de alojamiento, transporte o rutas. El diseño debe contemplar un esquema de optimización human-inthe-loop, donde el usuario interactúe con las sugerencias (aceptando o ajustando parámetros) para refinar continuamente el modelo de recomendación.
- Opción B, Asistente Virtual (Chatbot): Implementar un bot conversacional integrado que actúe como primer nivel de soporte interactivo para gestionar reprogramaciones, consultas de estado y problemas menores, delegando a la agencia de viajes preferida del usuario únicamente aquellos casos complejos.

### Quality Attributes
- Rendimiento (Performance) y Latencia: Las actualizaciones de viaje deben presentarse en la aplicación dentro de los 5 minutos posteriores a su generación por la fuente externa. El tiempo de respuesta desde la web debe ser de 800ms. En plataformas móviles, el primer despliegue de contenido (First-contentful paint) debe ocurrir en menos de 1.4 segundos.
- Disponibilidad (Availability): El sistema es de uso global y debe ser accesible en todo momento, tolerando un máximo de 5 minutos por mes de tiempo de inactividad no planificado.
- Escalabilidad (Scalability): La plataforma debe dimensionarse para soportar una base de 15 millones de cuentas, operando con 2 millones de usuarios activos semanales y soportando dramáticos picos de tráfico ante eventos disruptivos masivos.
- Interoperabilidad (Interoperability): Es imperativa una integración fluida con intercambios de aerolíneas, hoteles y arrendadoras a través de APIs estándar. Adicionalmente, el sistema debe interoperar con proveedores de correo para el escaneo de mensajes y con redes sociales para comparar itinerarios.
- Seguridad y Privacidad (Security): El sistema procesa información personal. Debe garantizarse el acceso seguro y autorizado a los correos, y permitir el uso compartido de itinerarios asegurando que solo personas específicas designadas puedan visualizarlos.
- Evolucionabilidad y Mantenibilidad (Evolvability): La arquitectura debe prever la integración futura de otros medios de transporte (trenes, autobuses, etc.). Apoyándose en el uso de ADRs y contratos (Spec-driven), el diseño general y el prototipo final deben exhibir una alta trazabilidad y facilitar evaluaciones futuras.
- Usabilidad (Usability) e Internacionalización: Se requiere una interfaz rica (aprovechando capacidades nativas como GPS en móviles) y el sistema debe estar preparado arquitectónicamente para operar en el mercado internacional (multiregión).