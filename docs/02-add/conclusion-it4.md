El LLM agregó otros QA y US que no atacó directamente, pero los usó para contextualizar sus elecciones.

El LLM planteó estilos que creemos que agrega complejidad a la solución que se puede realizar aplicando tácticas. Ports&Adapters ya está implementado de la iteración 2, y el filtro de seguridad es lo que logramos aplicando las tácticas.

Autenticar con tokens de vida corta para tener el servidor stateless para que el load balancer funcione tiene sentido, será agregado. En cada request, el cliente debe enviar la firma y vigencia del token

La táctica de limitar la exposicion de los itinerarios compartidos nosotros lo clasificamos dentro de "informar al usuario del posible intruso" y en la asignación de responsabilidades se aclaró que este mecanismo notificará la usuario si quiere o no dar permisos.

Adherirse a estándares es un nombre mas claro a la táctica de usar OAuth 2.0



Agregar:
(ADR12 DE LLM) - Authenticate actors con tokens firmados de vida corta y refresh (sin estado en el servidor)
(ADR14 DEL LLM, fusionar con el ADR15 nuestro)