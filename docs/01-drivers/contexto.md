# Diagrama de Contexto

```mermaid
flowchart TB
    Usuario["Usuario"]
    Web["Aplicación web"]
    App["Aplicación móvil"]

    Sistema(["Sistema Trotamundos"])

    Agencias["Agencias de terceros"]
    SistemasDeViajes["Sistemas de Viajes"]
    APIs["APIs estándar"]
    Correo["API Correo Electrónico"]
    Datos["Equipo de datos<br/>Análisis de viajes"]

    Usuario <--> Web
    Usuario <--> App

    Web <--> |"Solicitudes y respuestas"| Sistema
    App <--> |"Solicitudes y respuestas"| Sistema

    Sistema <--> |"Obtención de información"| APIs
    APIs <--> Agencias
    APIs <--> SistemasDeViajes

    Sistema <--> |"Detección automatica de Reservas"| Correo

    Sistema --> |"Recopilación de Analíticas"| Datos

    classDef core fill:#0000ff,color:#ffffff
    classDef actor fill:#808080,color:#ffffff
    classDef external fill:#ffff00,color:#000000
    class Sistema core
    class Usuario,Web,App,Datos actor
    class Agencias,SistemasDeViajes,APIs,Correo external
```

- Azul: Sistema propio
- Amarillo: Sistemas externos
- Gris: Actores
