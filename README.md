# Evaluacion_3_Intro_IA

## Automatización de Pedidos con IA 🤖🍔

Planteamiento del Problema:

El proceso de toma de pedidos en un restaurante de comida rápida a menudo es manual y propenso a errores. Esto puede llevar a pedidos incorrectos, demoras en el servicio y dificultades en el seguimiento y la gestión de la información. El objetivo de esta automatización es optimizar el proceso de pedido mediante la implementación de un sistema que:

1. Reciba los pedidos de los clientes a través de un chat.

2. Utilice un agente de IA (Groq) para procesar y estructurar la información del pedido.

3. Envíe una confirmación detallada del pedido al cliente a través de correo electrónico (Gmail)

4. Registre automáticamente los detalles del pedido en un archivo Excel para el inventario, la contabilidad y la gestión del restaurante.

Esta solución busca reducir la carga de trabajo manual, minimizar los errores y mejorar la eficiencia operativa y la experiencia del cliente.


Justificación de la Tecnología:

Para resolver este problema, la herramienta n8n es la elección ideal en comparación con una solución puramente de código. La ventaja principal de n8n es que, como plataforma de automatización de código bajo (low-code), nos permite construir flujos de trabajo complejos de manera visual y mucho más rápida.

1. Integraciones Nativas: n8n viene con nodos pre-construidos para servicios populares como Gmail y Microsoft Excel. Esto elimina la necesidad de escribir y mantener APIs y SDKs desde cero. Una solución de código requeriría que un desarrollador configure manualmente la autenticación (OAuth 2.0) y las solicitudes HTTP para cada servicio, un proceso que consume mucho tiempo.

2. Facilidad de Mantenimiento: El flujo de trabajo visual de n8n es fácil de entender y de modificar.  Si en el futuro es necesario cambiar la lógica de negocio, como añadir un servicio de SMS o integrar otro agente de IA, solo hay que añadir o modificar un nodo. En una solución de código, cada cambio podría requerir una reescritura significativa de la lógica de conexión y procesamiento de datos.

3. Reducción del Tiempo de Desarrollo: El desarrollo de un sistema similar desde cero con código implicaría escribir la lógica para el chat, la integración con Groq, la gestión de la autenticación de Gmail y Microsoft, el envío de correos, y la manipulación de archivos Excel. Con n8n, estos componentes se arrastran y conectan, lo que reduce el tiempo de desarrollo de semanas a días.

4. Menor Dependencia Técnica: Al ser una herramienta visual, cualquier persona con un conocimiento básico de la plataforma puede entender y mantener el flujo. Una solución de código requiere un desarrollador especializado que entienda todo el código fuente, aumentando la dependencia del talento técnico.

En resumen, mientras que una solución de código ofrece un control total, n8n proporciona la velocidad, la eficiencia y la flexibilidad necesarias para implementar este tipo de automatizaciones complejas de manera ágil y sostenible, sin sacrificar la funcionalidad.

Guía de Uso:

Funcionamiento del Flujo:

Este flujo de n8n está diseñado para ser iniciado por un WebHook al que el usuario envía la información del pedido a través del chat. El proceso es el siguiente:

1. El flujo comienza con un nodo de WebHook que recibe la solicitud de pedido.

2. Un nodo de Groq procesa el mensaje del usuario. Este agente extrae y estructura la información clave del pedido (ej. hamburguesa, papas, bebida, cantidad, precio total, etc.).

3. El flujo evalúa el precio total del pedido. Si el monto es mayor a $10.000, el flujo se detiene temporalmente y le solicita al usuario a través del chat que confirme el pago para continuar con el pedido. Esto permite un seguimiento más riguroso de las transacciones de alto valor.

4. Una vez que el pago se ha confirmado (o si el pedido es menor a $10.000), el flujo continúa en dos ramas paralelas:

* Rama 1: Un nodo de Gmail utiliza la información para componer y enviar un correo electrónico de confirmación al cliente.

* Rama 2: Un nodo de Microsoft Excel añade una nueva fila con los datos del pedido a una hoja de cálculo designada, facilitando el seguimiento para el restaurante.

Instrucciones de Configuración:

Para poner en marcha este flujo, necesitas configurar las siguientes credenciales:

1. Credenciales de Groq:

* Necesitas tu clave de API de Groq.

2. Credenciales de Gmail:

* Debes configurar un nodo de Gmail con tu cuenta. n8n te guiará a través del proceso de autenticación de OAuth 2.0 para que puedas dar permiso a la aplicación para enviar correos electrónicos en tu nombre.

3. Credenciales de Microsoft Excel:

* De manera similar, debes configurar un nodo de Microsoft Excel con tu cuenta de Microsoft. n8n te guiará para autenticar tu cuenta y seleccionar el archivo de Excel donde deseas almacenar los pedidos.

Pasos para el Usuario Final:

1. El usuario debe enviar un mensaje a través del chat con el pedido deseado.

2. El sistema pedirá al usuario que se autentique con su cuenta de Gmail para recibir la confirmación.

3. Si el pedido es de un monto alto, se le solicitará al usuario que confirme su pago a través del chat.

4. El sistema automáticamente enviará los datos del pedido al flujo de n8n, que ejecutará la lógica descrita para enviar el correo electrónico y registrar el pedido en el archivo de Excel.
