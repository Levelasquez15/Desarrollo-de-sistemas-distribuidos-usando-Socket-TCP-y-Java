# Decisiones Técnicas

Durante el desarrollo de las aplicaciones Cliente y Servidor descritas en la guía, se han tomado las siguientes decisiones técnicas:

1. **Uso de Sockets TCP en lugar de UDP:**
   - **Motivo:** El cálculo del IMC requiere que los datos de peso y altura lleguen correctamente, y que la respuesta vuelva de forma confiable. TCP garantiza que no haya pérdida de paquetes y que el orden se mantenga.

2. **Multihilo en el Servidor (Multithreading):**
   - **Motivo:** Para evitar que el servidor se bloquee atendiendo a un solo cliente, se decidió extender la clase `Thread` en `SubProcesoCliente`. Cada vez que un cliente se conecta mediante `servicio.accept()`, el servidor delega la comunicación de ese cliente a un hilo independiente.

3. **Uso de `DataInputStream` y `DataOutputStream`:**
   - **Motivo:** Facilitan el envío y recepción de datos primitivos de Java a través de la red de manera sencilla (`writeFloat`, `readFloat`, `writeUTF`, `readUTF`), en lugar de procesar los flujos de bytes manualmente.

4. **Uso de un `HashMap` para el registro de clientes (`listaDeClientes`):**
   - **Motivo:** Permite mantener un registro en memoria de los clientes actualmente conectados en el servidor. La dirección IP de cada cliente se utiliza como llave (`String`), y el objeto `SubProcesoCliente` como valor, lo que facilita remover a un cliente específico cuando se desconecta.

5. **Separación de Lógica y Vista:**
   - **Motivo:** Se creó la clase `CalculoImc` independiente de los Sockets y de la interfaz gráfica. Esto permite reutilizar la lógica de cálculo sin estar atada a los eventos de los botones o a la recepción de red.

6. **Implementación de `Serializable` en el Modelo:**
   - **Motivo:** Aunque la comunicación demostrada en los hilos utiliza principalmente el envío de primitivos (`Float`, `String`), la clase modelo `CalculoImc` implementa la interfaz `Serializable`, permitiendo futuras expansiones donde se envíen objetos completos a través de la red (por ejemplo usando `ObjectOutputStream`).
