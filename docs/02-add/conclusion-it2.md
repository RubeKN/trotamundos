El LLM optó por elegir más drivers sobre el performance (Web y Mobile), tiene sentido su elección porque forma parte de la velocidad con la que llegan los datos. Nosotros no lo tomamos pensando esa parte unicamente como parte del front-end. (Incluso, el LLM en el paso 7 dice que el escenario QA04, no lo abordó correctamente y QA03 quedo parcialmente cubierto)

El LLM pensó en la misma idea de que las lecturas son prioritarias para cumplir las medidas de respuesta de los drivers, al igual que la idea de tener réplicas + balanceador de carga (Lo llamó "Service-Based: servicios de grano grueso y sin estado, con balanceador y autoscaling", pero es la misma idea).

Acerca de la priorización de lecturas por sobre escrituras, nosotros usamos una cola de prioridad por tipo de operación y FIFO. El LLM usó el estilo CQRS, el cual separa las lecturas y escrituras en dos modelos distintos, es la misma idea que planteamos nosotros, pero le dió el nombre al estilo.

El LLM sugirió particionar la base de datos por viajeroID, el equipo no sabía que esto se podía hacer pero es una lógica para asegurar que un usuario solo consulte a única replica.

ADRs a agregar:
Parte del ADR-06 de división de réplicas por idViajero