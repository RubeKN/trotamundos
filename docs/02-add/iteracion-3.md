# Iteración 2 - Escalabilidad, Rendimiento y Persistencia en "Trotamundos"

## PASO 2 - Objetivo de la Iteración

Escalar la arquitectura del sistema Trotamundos para soportar una alta concurrencia de usuarios y un volumen proyectado de 15 millones de cuentas, garantizando disponibilidad, escalabilidad y rendimiento de operaciones.

**Drivers a desarrollar en la iteración:**

* QA05 - Cantidad de cuentas
* QA06 - Actividad semanal
* QA07 - Picos de trafico
* ADR2 - Centralidad del Server (concern iteración-1)

## PASO 3 - Descomposición

La lógica de trotamundos es lo que está con mayor incertidumbre. Se decomponen los componentes internos del mismo sobre como realizar las operaciones (consultas y escrituras manuales) de los usuarios.

## PASO 4 - Aplicando conceptos de diseño a los drivers seleccionados

**Alternativas propuestas**

| Alternativa | Pros | Contras | Drivers relacionados |
| --- | --- | --- | --- |
| Load Balancer de usuarios | Ante una sobrecarga de un servidor, se puede mantener la disponibilidad y performance estable | Complejidad en la sincronizacion de sesiones | QA06, QA07 |
| Cola de Prioridad | Mejores tiempos de respuesta ante consultas al dashboard | Introduce intermediarios, puede retrasar las escrituras demasiado (starvation) | QA06, QA07 |
| Procesamiento secuencial sin colas | Sin capas intermedias, mejor performance en casos generales | No permite agregar concurrencia, bloqueo de mucho tiempo ante grandes escrituras | QA07 |
| Base de Datos Relacional + Caché | Soporta lecturas masivas, simplicidad en el modelo de datos (vs NoSQL) | Costo en replicación y almacenamiento de grandes volumenes de datos | QA05 |
| Base de Datos NoSQL | Flexibilidad y mejor escalamiento horizontal, soporte nativo de grandes volumenes de datos | Mayor curva de aprendizaje para el equipo, dificil realizar referencias | QA05 |


Para satisfacer tanto los QA sobre las operaciones de usuarios como los de escalabilidad en usuarios y en pos de dinamizar la arquitectura Cliente-Servidor descentralizando la lógica, se opta por un diseño que combina balanceo de carga y priorización de operaciones. Además se toma una base relacional para aprovechar su simplicidad y uso general y se lo combina con una caché.

Elegidos: "Load balancer de usuarios", "Cola de prioridad", "Base de datos relacional + Caché"

## PASO 5 - Instanciar elementos, asignar responsabilidades y definir interfaces

El load balancer actua como gateway al trafico de usuarios, distribuyendo dinamicamente en distintas instancias de servidores.

El servidor que trate los usuarios debe procesar su solicitud y encolarla en la cola de prioridad la cual clasifica como prioritarias las lecturas (son mas rápidas) y luego las escrituras manuales.

Para aprovechar la separación de lecturas y escrituras se coloca una cache para almacenar datos de consultas frecuentes, evitando acceder a la base en cada lectura. Para que esto funcione, las escrituras deben realizarse sobre una base primaria que mantenga consistente las replicas (Sobreescribiendo) y la caché (invalidando)


## PASO 6 - Vistas

Descomposición del sistema:

```mermaid
graph TD
    A((Trotamundos)) ---- B((Conexión APIs))
    A ---- C((Lógica Trotamundos))
    C ---- H((Manejo de usuarios))
    C ---- D((Operaciones del usuario))
    C ---- G((Presentación dashboard))
    D ---- E((Lectura de arreglos))
    D ---- F((Escritura manual))
    C ---- I((Funcionalidades adicionales))

```

Vista de arquitectura tratada en la iteracion:

```mermaid
flowchart TD
    %% Clientes externos
    subgraph Clients["Clientes / Dispositivos"]
        WebUI["Web App / Mobile App"]
    end

    %% Capa de Entrada y Escalabilidad
    subgraph EdgeLayer["Capa de Balanceo"]
        LB["Load Balancer"]
    end

    %% Capa de Backend / Servidores en Réplicas
    subgraph ApplicationTier["Servidores de Aplicación"]
        S1["Backend Instance 1<br/>(Trotamundos API)"]
        S2["Backend Instance 2<br/>(Trotamundos API)"]
        Sn["Backend Instance N<br/>(Auto-scaling)"]
    end

    %% Capa de Encolamiento y Priorización
    subgraph QueueTier["Capa de Encolamiento y Priorización"]
        Queue["Priority Queue<br/>---<br/>1. Prioridad Alta: Lecturas (Read FIFO)<br/>2. Prioridad Baja: Escrituras (Write FIFO)"]
    end

    %% Capa de Rendimiento, Caché y Persistencia
    subgraph DataTier["Capa de Datos y Caché"]
        Cache[("Caché")]
        DB_Primary[("Primary DB<br/>(Escrituras)")]
        DB_Replica[("DB Read Replicas<br/>(Lecturas secundarias)")]
    end

    %% Flujos y Conexiones

    %% 1. Tráfico de entrada
    WebUI --> LB
    LB -->|"Distribución de Tráfico"| S1
    LB -->|"Distribución de Tráfico"| S2
    LB -->|"Distribución de Tráfico"| Sn

    %% 2. Envío a la cola de priorización
    S1 & S2 & Sn -->|"Encola operaciones (Lecturas/Escrituras)"| Queue

    %% 3. Procesamiento de la cola según reglas
    Queue -->|"Lecturas"| Cache
    Queue -->|"Escrituras"| DB_Primary

    %% 4. Invalidación de caché en escrituras
    DB_Primary -.->|"Invalida datos cambiados"| Cache

    %% 5. Respaldo de lectura y replicación
    Cache -.->|"Cache Miss"| DB_Replica
    DB_Primary ==>|"Replicación de Datos"| DB_Replica

```

## PASO 7 - Revisar la aplicación del método

En esta segunda iteración, se trataron temas de escalabilidad como prioritarios. Los tacticas seleccionadas ayudan a satisfacer los 3 QA seleccionados, cada tactica se adapta para poder cumplir con el QA que beneficia sin perjudicar fuertemente al resto.

En el diagrama de descomposicion se ve abordado la parte principal de operaciones que puede hacer el usuario sobre la base de datos. Para tener en cuenta, aun no se trató como asegurar la latencia tanto a web como mobile, aunque las decisiones de esta iteración afecten positivamente los requerimientos de performance de estos escenarios.