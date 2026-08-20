# Errores Conocidos y Manejo de Excepciones

En base a la arquitectura y código descrito en la guía, los siguientes son errores conocidos, excepciones frecuentes y su forma de mitigación:

## 1. Errores de Reglas de Negocio
- **Causa:** Datos ingresados no válidos por el usuario (ej. Peso <= 0 o Altura <= 0).
- **Mensaje:** `"ERROR: El peso y la altura deben ser mayores que 0"`
- **Manejo:** Validado internamente en el método `getImc()` de la clase `CalculoImc`. Si ocurre, el cálculo se detiene y se devuelve el mensaje de error al cliente de manera amigable.

## 2. Errores de Conexión del Servidor
- **Causa:** El puerto definido ya está siendo ocupado por otra aplicación, o el programa no tiene permisos del sistema operativo para abrir el socket de escucha.
- **Mensaje (Consola/Log):** `"ERROR al abrir el puerto [numero]"`
- **Manejo:** Capturado a través de una `IOException` al intentar inicializar `new ServerSocket(puerto)`. La interfaz revierte el estado visual a "OFF LINE" y habilita nuevamente el botón de iniciar.

## 3. Errores de Conexión del Cliente
- **Causa:** El cliente intenta conectarse a una IP o Puerto donde no hay un servidor escuchando, o el servidor está apagado.
- **Mensaje (UI):** `"ERROR AL CONECTAR"` (lanzado en consola) o `"Falla en la conexion"` (en un cuadro de diálogo).
- **Manejo:** Se captura `IOException` (o `UnknownHostException` / `ConnectException`) al intentar ejecutar `new Socket(ip, puerto)`. Se debe mostrar una alerta al usuario.

## 4. Errores de Comunicación Durante el Tráfico de Datos
- **Causa:** La conexión de red se interrumpe físicamente, el servidor se apaga abruptamente, o el cliente se cierra a la fuerza mientras se intercambian flujos.
- **Mensajes:** 
  - `"Error al capturar datos del cliente [IP]"`
  - `"Error al enviar datos al cliente [IP]"`
  - `"Error al leer datos del cliente [IP]"`
- **Manejo:** Estas anomalías son capturadas mediante `IOException` al utilizar `readFloat()`, `writeUTF()`, etc. En el servidor, el bloque `catch` procede a forzar el cierre del socket y se remueve al cliente infractor del mapa (`ServidorTcp.listaDeClientes.remove(ip)`). En el cliente se debe notificar al usuario.

## 5. Acciones Fuera de Secuencia
- **Causa:** El usuario en el cliente intenta presionar el botón "Calcular" sin haber establecido primero la conexión con el servidor.
- **Mensaje:** `"Cliente OffLine, Conecte con el Servidor"`
- **Manejo:** La interfaz del cliente valida el estado del socket (mediante variables lógicas o métodos como `servidor.isConnected()`) antes de intentar enviar los datos por la red.
