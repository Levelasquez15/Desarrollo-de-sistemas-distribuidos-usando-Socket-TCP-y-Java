# Flujo de Trabajo (Workflow)

El flujo de trabajo descrito en la guía para la construcción de los sistemas distribuidos es el siguiente:

## Fase 1: Entorno y Herramientas
1. Descargar e instalar Java SE Development Kit (JDK 8).
2. Descargar e instalar el IDE Apache NetBeans (versión 12+).
3. Configurar complementos adicionales para modelado (opcional, como PlantUML).

## Fase 2: Desarrollo de la Aplicación Servidor
1. **Creación del Proyecto:** Crear un proyecto `Java Application` en NetBeans (ej. `ServidorTcpImc`).
2. **Definición de Paquetes:** Crear los paquetes lógicos (`modelo`, `servidor`, `vistas`).
3. **Lógica de Negocio:**
   - Crear la clase `CalculoImc` que maneja las reglas de negocio (recibe peso/altura y retorna resultados y mensajes).
4. **Capa de Red (Sockets):**
   - Crear la clase `ServidorTcp` (hereda de `Thread`) que contiene un `ServerSocket` para escuchar en un puerto específico (ej. 9007) y aceptar clientes en un bucle continuo.
   - Crear la clase `SubProcesoCliente` (hereda de `Thread`) que se encarga de manejar la comunicación individual con un cliente que ya se conectó (recibir parámetros y enviar respuestas).
5. **Capa de Presentación (Vista):**
   - Crear la interfaz `VentanaPrincipal` (hereda de `JFrame`).
   - Añadir botones y campos para iniciar/detener el servidor, definir el puerto y visualizar la bitácora (Log de conexiones).
   - Conectar los eventos de la vista con la instanciación e inicio de `ServidorTcp`.

## Fase 3: Desarrollo de la Aplicación Cliente
1. **Creación del Proyecto:** Crear un nuevo proyecto `Java Application` en NetBeans (ej. `ClienteTcpImc`).
2. **Definición de Paquetes:** Crear paquetes lógicos (`cliente`, `vistas`).
3. **Capa de Presentación (Vista):**
   - Crear la interfaz `VentanaPrincipal` usando el diseñador.
   - Añadir paneles de "Conexión" (IP y Puerto del Servidor) y "Calculo IMC" (Peso y Altura).
4. **Capa de Red y Lógica (Cliente):**
   - Instanciar un `Socket` apuntando a la IP y Puerto proporcionados por el usuario.
   - Configurar flujos de datos (`DataOutputStream`, `DataInputStream`) asociados al Socket.
   - Mapear el evento del botón "Calcular" para que recolecte los datos de la GUI, los envíe al servidor, lea la respuesta y actualice la interfaz gráfica con el resultado.

## Fase 4: Pruebas del Sistema (Testing)
1. Ejecutar el proyecto de la Aplicación Servidor.
2. Iniciar el servicio desde la interfaz gráfica y verificar que escuche en el puerto deseado.
3. Ejecutar una o múltiples instancias de la Aplicación Cliente.
4. Conectar los clientes usando la dirección IP local (`localhost` o IP de red) y el puerto.
5. Ingresar datos de prueba, solicitar el cálculo y confirmar que el servidor procesa y devuelve los valores correctos en cada instancia cliente.
