# Plan de Iteraciones ADD - Trotamundos

## 1.- Alcance

Este plan organiza la primera ronda de diseño (prototipo básico) en 5 iteraciones, siguiendo los pasos 2 a 7 de ADD.md por cada iteración. El Paso 1 (Review inputs) se realiza una sola vez al inicio de la ronda y ya está cubierto por `ArchitecturalDrivers.md` y el modelo de dominio de `Architecture.md`.

Criterios usados para ordenar las iteraciones:

- La iteración 1 estructura el sistema y fija las decisiones de mayor impacto y más difíciles de revertir (estilo arquitectónico, integración con externos, disponibilidad).
- Las iteraciones 2 y 3 abordan el resto de los drivers de importancia alta para el negocio, priorizando los que respaldan directamente la propuesta de valor (Dashboard, detección de reservas e integración con terceros).
- Las iteraciones 4 y 5 cubren funcionalidades secundarias y drivers de importancia media o baja.
- Las restricciones (C1, C2) y el concern de neutralidad tecnológica aplican a todas las iteraciones: cada decisión se registra como MADR y los elementos se definen mediante interfaces/contratos genéricos.

## 2.- Plan de iteraciones

| Iteración | Objetivo principal | Drivers a abordar |
| --- | --- | --- |
| **1** | **Estructuración inicial del sistema.** Definir la arquitectura base: estilo arquitectónico general, descomposición de alto nivel, clientes web y móvil, flujo de datos para consolidar reservas en el Dashboard, mecanismo de ingesta desacoplado para fuentes externas (APIs de terceros y proveedores de correo) y tácticas básicas de disponibilidad y latencia de actualizaciones. | US01 - Dashboard<br>QA01 - Presentar actualizaciones<br>QA04 - Inactividad no planificada<br>QA14 - APIs estándar<br>QA15 - Proveedor email |
| **2** | **Escalabilidad y rendimiento del núcleo.** Refinar los elementos de la iteración 1 para soportar el volumen objetivo (15 M de cuentas, 2 M de usuarios semanales, 500 req/s y picos de 2500 req/s): estrategia de datos y particionamiento, caché, escalado horizontal, balanceo y amortiguación de picos. Asegurar los tiempos de respuesta de web y primer contenido móvil. | QA05 - Cantidad de cuentas<br>QA06 - Actividad semanal<br>QA07 - Picos de tráfico<br>QA02 - Tiempo de respuesta web<br>QA03 - Primer contenido mobile |
| **3** | **Pipeline de reservas, seguridad de acceso y extensibilidad.** Completar el flujo de negocio principal: detección de reservas por correo, filtros y whitelist, actualización continua desde terceros (altas, cambios, cancelaciones) y deduplicación. Asegurar el acceso al correo (cifrado y autorización) y volver extensible el sistema a nuevos medios de transporte y a nuevos países. | US02 - Detección automática de reservas<br>US03 - Filtros y whitelists<br>US04 - Integración con terceros<br>QA08 - Acceso email<br>QA10 - Nuevos medios de transporte<br>QA13 - Multiregión |
| **4** | **Colaboración, resolución de problemas y analítica.** Diseñar el compartir itinerarios con autorización estricta, la interoperabilidad con redes sociales, la derivación de incidencias a la agencia de viajes preferida y la captura de datos analíticos para monetización con su API interna. | US05 - Resolución de problemas<br>US06 - Analítica de datos<br>US07 - Compartir reservas<br>QA09 - Itinerarios compartidos<br>QA16 - Proveedores redes |
| **5** | **Experiencia de usuario y recomendación (prioridad baja, condicional).** Refinar la UI centrada en el viaje, el uso de capacidades nativas del dispositivo y el sistema de recomendación con bucle human-in-the-loop. Se ejecuta solo si el tiempo del prototipo lo permite; de lo contrario, queda como backlog para la siguiente ronda. | US08 - Sistema de recomendación<br>QA11 - UI simple centrada en viaje<br>QA12 - Aprovechar capacidades nativas |

## 3.- Cobertura de drivers

| Tipo | Drivers | Iteración |
| --- | --- | --- |
| User stories | US01 | 1 |
| | US02, US03, US04 | 3 |
| | US05, US06, US07 | 4 |
| | US08 | 5 |
| Quality attributes | QA01, QA04, QA14, QA15 | 1 |
| | QA02, QA03, QA05, QA06, QA07 | 2 |
| | QA08, QA10, QA13 | 3 |
| | QA09, QA16 | 4 |
| | QA11, QA12 | 5 |
| Constraints y concerns | C1, C2, neutralidad tecnológica | Transversales (todas) |

## 4.- Justificación del orden

- **Iteración 1.** Contiene los drivers de mayor dificultad técnica combinados con alta importancia (QA01, QA04, QA15) más el requisito central del negocio (US01) y la integración con APIs estándar (QA14). Son los que más condicionan la estructura: las decisiones de ingesta asíncrona, desacoplamiento de externos y redundancia son costosas de cambiar después.
- **Iteración 2.** QA07 (alta/alta) y QA06, QA05 (alta importancia) dependen de la estructura de la iteración 1 y se resuelven refinando sus elementos. QA02 y QA03 se agrupan aquí porque comparten las tácticas de latencia y caché.
- **Iteración 3.** Completa los flujos que generan el valor diferencial (US02, US03, US04) sobre los cimientos ya diseñados, y cubre los restantes drivers de alta importancia (QA08, QA10, QA13).
- **Iteración 4.** Funcionalidades de colaboración y soporte con menor impacto en la estructura base. US06 se ubica aquí porque la analítica se apoya en `EventoReserva` y `RegistroAnalitico`, que ya existen tras las iteraciones previas.
- **Iteración 5.** Drivers de importancia media/baja, sin tolerancia a retrasos que afecten el prototipo. US08 depende del historial acumulado, por lo que es razonable dejarlo al final.

## 5.- Criterios de cierre por iteración (Paso 7 de ADD)

Al finalizar cada iteración se debe responder: ¿se cumplió la meta?, ¿qué drivers quedan parcialmente abordados?, ¿qué riesgos o incertidumbres surgieron?, ¿se requiere reordenar o añadir una iteración? Los resultados se registran en el documento de arquitectura (secciones Diagrams, Interfaces y Design decisions) y en MADR.
