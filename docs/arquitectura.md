# Arquitectura del Sistema

El proyecto descrito en la guía se basa en una arquitectura **Cliente-Servidor** distribuida, utilizando **Sockets TCP** para la comunicación en red y desarrollada en **Java**.

## Componentes Principales

### 1. Aplicación Servidor
Actúa como un servicio que procesa las peticiones de los clientes.
- **Puerto de Escucha:** Abre un puerto lógico de red específico (por defecto 9007).
- **Concurrencia:** Es capaz de aceptar, atender y procesar solicitudes de conexión provenientes de múltiples instancias de aplicaciones clientes simultáneamente, utilizando Hilos (`Thread`).
- **Lógica de Negocio:** Recibe datos de entrada (peso y altura), calcula el Índice de Masa Corporal (IMC) y determina el estado de salud de la persona.
- **Respuesta:** Devuelve el valor del IMC calculado y un mensaje descriptivo al cliente que realizó la solicitud.
- **Interfaz Gráfica:** Posee un panel para iniciar/detener el servicio y una bitácora (log) que muestra la actividad de los clientes conectados.

### 2. Aplicación Cliente
Actúa como la interfaz de usuario para enviar datos al servidor.
- **Conexión:** Permite al usuario ingresar la dirección IP y el número de puerto del servidor para establecer la conexión.
- **Entrada de Datos:** Una vez conectado, provee un formulario para que el usuario ingrese su peso y altura.
- **Interacción:** Envía estos datos a través del socket hacia el servidor.
- **Visualización:** Recibe y muestra en pantalla el resultado del IMC y el mensaje provisto por el servidor.

## Protocolo de Comunicación
- Se utiliza el protocolo de transporte **TCP** (Transmission Control Protocol) para garantizar la entrega fiable, ordenada y sin errores del flujo de datos entre el cliente y el servidor.
- El intercambio de datos se realiza utilizando flujos de entrada y salida de datos (`DataInputStream` y `DataOutputStream`), permitiendo el envío de tipos primitivos (como `float` para peso/altura/IMC) y cadenas de texto (como `String` en formato UTF para mensajes).
