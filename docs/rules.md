# Reglas del Sistema

Al desarrollar, extender y operar este proyecto de Sockets TCP, se deben respetar las siguientes reglas fundamentales establecidas en la guía base:

## Reglas de Inicialización
1. **Precedencia de Servicios:** La Aplicación Servidor siempre debe ejecutarse, configurarse y estar en estado "ONLINE" (escuchando el puerto) ANTES de que cualquier Aplicación Cliente intente establecer una conexión.
2. **Puertos Emparejados:** Tanto el servidor como el cliente deben estar configurados explícitamente para comunicarse a través del mismo número de puerto (ej. `9007`).

## Reglas de Arquitectura de Red (Sockets)
3. **No Bloquear el Hilo Principal (GUI):** Las operaciones prolongadas de red, como escuchar por nuevas conexiones (`accept()`) o esperar datos de entrada (`read()`), bloquean la ejecución. Éstas nunca deben estar en el Hilo de la Interfaz Gráfica (Event Dispatch Thread). Siempre se deben delegar a Hilos (`Thread`) secundarios o trabajadores.
4. **Un Hilo por Cliente:** El servidor debe asignar un hilo de ejecución individual y exclusivo (`SubProcesoCliente`) por cada conexión activa de cliente para asegurar que múltiples usuarios puedan ser atendidos de forma concurrente sin que unos bloqueen a otros.
5. **Cierre Ordenado de Recursos:** Toda conexión (`Socket`) y flujo asociado (`DataInputStream`, `DataOutputStream`) debe cerrarse invocando el método `.close()` explícitamente tan pronto como la tarea finalice o cuando se detecte una anomalía (capturada en los bloques `catch` / `finally`), para evitar fugas de recursos y conexiones huérfanas a nivel de sistema operativo.

## Reglas de Consistencia
6. **Sincronización del Estado de Conexión:** La Interfaz Gráfica (tanto del cliente como del servidor) siempre debe reflejar fielmente el estado actual de las conexiones de red (ONLINE, OFFLINE, Conectado, Desconectado) utilizando retroalimentación visual (ej. cambio de colores y logs en pantalla).
7. **Independencia del Modelo:** Las reglas del cálculo del índice de masa corporal y sus rangos de validación médica (bajo peso, normal, sobrepeso) deben existir puramente dentro de las clases del paquete `modelo` (ej. `CalculoImc`), manteniéndose agnósticas de que los datos llegaron por un Socket o desde una Interfaz.
8. **Seguridad de Tipos en Sockets:** Se debe mantener el orden estricto de los tipos de datos al enviar y recibir. Si el cliente escribe primero un `float` (peso) y luego otro `float` (altura), el servidor debe obligatoriamente leer dos iteraciones de `readFloat()` en ese mismo y exacto orden, o la trama de red arrojará errores de formato.
