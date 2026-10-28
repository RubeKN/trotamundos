El paso 4 tuvo las mismas movilizacion que nos hicieron pensar durante la discusión sobre que estilos elegir
- Fuentes externas a diferentes tiempos que nuestro sistema
- Si se cae una fuente externa no debe caerse el dashboard
- Los datos vienen en formatos distintos segun el proveedor

La idea del estilo Publisher-Subscriber es la misma que tomamos nosotros. Desacoplar los 3ros con el dashboard. El LLM uso la palabra "broker" a lo que nosotros dijimos que es el middleware que hace requests a los 3ros y alimenta el bus, ademas de hacer la normalizacion de datos.

El estilo service-based no lo consideramos como servicios aun al resto del componentes, aun no pensamos en el despliegue del sistema. Pero la idea de abstract common services nosotros la imaginamos dentro de el estilo ports&adapters, donde cada proovedor está detras de una interfaz comun, evitando que toquen al logica.

La tactica circuit breaker se puede adaptar con un timer, ante una falla de un proveedor se prueba con tiempos incrementales, si tras varios errores sigue fallando el proveedor se informa al usuario que no se puede establecer la conexion con ese proveedor.

La tactica detect and recover, habla sobre el disponibilidad en despliegue, que aun no había sido considerada por el grupo.

Los riegos que indica el LLM son correctos, el correo se debe sondear en intervalos cortos para asegurar los 5 minutos de tope final (El LLM sugiere 2 minutos como maximo). EL dashbord puede tener retraso con los datos en los distintos proveedores, pero el QA pide que se mantenga actualizado con 5 minutos, ya está contemplado. El broker reuqiere redundancia para que no caiga la principal funcionalidad del sistema.

Las vistas del LLM, especialmente V1 intenta mostrar todo el sistema en una misma, nosotros optamos por vistas mas reducidas en el objetivo de la iteración

DECISIONES A INCORPORAR:
ADR-004, ADR-005
Las ADRs sobre deployment se excluyen de esta iteración, no era el foco principal de esta iteracion.