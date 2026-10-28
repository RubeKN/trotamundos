# Iteración 4 - Tratamiento de seguridad

## PASO 2 - Objetivo de la Iteración
A estas alturas del diseño del sistema, nos parece acorde abordar la confianza y seguridad del usuario en el uso de nuestra aplicación web.

**Drivers a desarrollar en la iteración:**
- QA08 - Security: Acceso email
- QA09 - Security: Itinerarios compartidos
- QA15 - Interoperability: Proveedores email


## PASO 3 - Descomposición
Con una buena base de la lógica ya abordada, es fundamental tener un control de que datos se muestran o tranfieren entre usuarios, por lo que controlaremos las situaciones de riesgo que puedan llegar a crearse.


## PASO 4 - Aplicando conceptos de diseño a los drivers seleccionados

**Alternativas propuestas:**

| Alternativa | Pros | Contras | Drivers relacionados |
|---|---|---|---|
| Encriptar datos | Protege la información en la base de datos, protege los datos en tránsito | Sobrecosto computacional por cifrado/descifrado, requiere gestión de claves | QA08, QA09 |
| Detectar intruso | Permite rechazar amenazas a tiempo | Overhead por chequeo ante cada acceso, agrega necesidad de una base de datos con información de comportamiento malicioso | QA08 |
| Integridad de mensaje | Asegura que los mensajes e itinerarios no sean alterados en tránsito | Aumenta la latencia en la integridad del mensaje, complejidad en gestión de firmas/claves | QA08, QA09 |
| Informar al usuario del posible intruso | El usuario tiene consciencia de la situación, la decisión es ajena al sistema pero fácil de implementar | Depende de la respuesta activa del usuario, posible fatiga de notificaciones | QA08, QA09 |
| Autenticar usuario | Rápido de validar, asegura la identidad antes de otorgar acceso | Requiere gestión segura de sesiones/tokens | QA08 |
| Solicitar autorización del usuario para acceder a su email | Decisión del usuario, control de los mensajes recibidos | El usuario puede perder funcionalidades si rechaza el permiso | QA08, QA15 |

Para satisfacer los requerimientos del sistema, creemos conveniente optar por las siguientes opciones:
"Encriptar datos", "Informar al usuario del posible intruso", "Autenticar usuario" y "Solicitar autorización del usuario para acceder a su email".

Creemos que las opciones "Detectar intruso" e "Integridad de mensaje" no las creemos las mejores opciones debido a que sus contras agregan demasiada funcionalidad, lo que empeora el funcionamiento general del sistema.


## PASO 5 - Instanciar elementos, asignar responsabilidades y definir interfaces
Si es la primera vez que un usuario quiere iniciar en el sistema, se le solicitará permisos para interactuar con su cuenta de email, mediante la utilización de OAuth, y para iniciar, los usuarios deben acceder con email y contraseña. A la hora encriptar los datos, se utilizara https, con lo que solo es necesario tener los credenciales para poder utilizarlo, y mediante la notificación al usuario sobre una situación que excede en decisiones al servidor, se le darán dos opciones: aceptar la solicitud, en caso de que el usuario quiera que el usuario aún no autorizado acceda al itinerario propio, o rechazar la solicitud, en caso de que sea una persona que el usuario considere no apropiada para acceder al mismo.


## PASO 6 - Documentación

### Vistas

**Vista comportamental:**

```mermaid
    sequenceDiagram
    autonumber
    actor U as Usuario [ U ]
    actor UI as Usuario Invitado / No Autorizado [ UI ]
    participant C as Cliente (Frontend)
    participant S as Servidor (Backend)
    participant OAuth as Proveedor de Email (OAuth2)
    participant BD as Base de Datos

    %% 1. Autenticación y Consentimiento inicial
    rect rgb(240, 240, 240)
    note over U, OAuth: 1. Autenticación y Autorización de Email (HTTPS / TLS)
    U->>C: Ingresa Email y Contraseña
    C->>S: POST /login (Cifrado vía HTTPS)
    S->>BD: Validar credenciales
    BD-->>S: Credenciales válidas
    
    alt Primera vez en el sistema
        S-->>C: Requiere permisos de Email
        C->>OAuth: Solicitar consentimiento de acceso al Email
        OAuth-->>U: Mostrar pantalla de permisos
        U->>OAuth: Otorga permisos
        OAuth-->>C: Código de autorización / Token
        C->>S: Enviar Token de Email
        S->>BD: Guardar tokens e información de perfil
    end
    S-->>C: Sesión iniciada con éxito (JWT / Session Token)
    end

    %% 2. Intento de acceso a itinerario no autorizado y Notificación
    rect rgb(230, 240, 250)
    note over UI, U: 2. Solicitud de Acceso e Intervención del Usuario
    UI->>C: Solicita ver el itinerario de U
    C->>S: GET /itinerarios/{id} (Cifrado vía HTTPS)
    S->>BD: Verificar permisos de UI sobre el itinerario
    BD-->>S: UI no está autorizado

    S->>U: Enviar notificación de solicitud de acceso
    note over U: Decisiones que exceden la lógica del servidor

    alt Opción 1: Aceptar solicitud
        U->>S: Responder "Aceptar"
        S->>BD: Registrar a UI en la lista de acceso permitido
        S-->>C: Permiso concedido
        C-->>UI: Muestra el itinerario
    else Opción 2: Rechazar solicitud
        U->>S: Responder "Rechazar"
        S->>BD: Registrar rechazo / Bloquear acceso
        S-->>C: Acceso denegado
        C-->>UI: Muestra mensaje de error (No autorizado)
    end
    end
```

Se muestran en un diagrama de secuencias las posibles alternativas de un usuario intentando ver un itinerario compartido (con o sin login, con o sin autorización, el sistema de autorización en sí mismo).

### ADRs generados

- ADR12 - Encriptación HTTPS
- ADR13 - Detección de Viajero no habilitados a ver itinerario
- ADR14 - Autenticación de Viajero
- ADR15 - Solicitar autorización para conectar correo electrónico

## PASO 7 - Revisar la aplicación del método

En esta iteración, se abordaron las qa08 y qa09 referidas al escenario de seguridad, y la qa15 refererida al escenario de interoperabilidad. Tratamos de dar un soporte seguro y de confianza al usuario que se adentra en los servicios del sistema, siendo transparentes con las decisiones. En estos casos, el usuario toma un rol participativo, con lo cual se requiere la interacción entre la capa de cliente y la capa de servidor. Para próximas iteraciones, queda pendiente la parte de presentación.