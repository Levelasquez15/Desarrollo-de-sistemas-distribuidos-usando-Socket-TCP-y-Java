# Manual de Usuario: ¿Cómo funciona el sistema IMC?

Este documento explica paso a paso cómo operar las aplicaciones Servidor y Cliente que hemos construido basándonos en la guía.

## 1. Concepto Básico
El sistema consta de dos programas independientes que se comunican a través de tu red (o dentro de tu misma computadora) usando Sockets TCP:
- **El Servidor:** Espera pacientemente a que los clientes se conecten. Su única labor es recibir un `peso` y una `altura`, calcular matemáticamente el Índice de Masa Corporal (IMC) y devolver el resultado.
- **El Cliente:** Es la pantalla que usa el usuario final. Se conecta al servidor, envía sus datos de salud y muestra la respuesta en pantalla.

## 2. Pasos para iniciar y probar el sistema

### Paso A: Arrancar el Servidor
1. Ejecuta la aplicación del Servidor (`ServidorTcpImc`).
2. Verás una ventana llamada **"SERVIDOR IMC"**.
3. Asegúrate de que el puerto sea `9007`.
4. Haz clic en el botón verde **"INICIAR"**.
5. Si vas a la pestaña **"LOG DE CONEXIONES"**, deberías ver un mensaje que dice: `Servidor disponible en el Puerto 9007`. 
   *Nota: El servidor debe estar en estado ONLINE antes de abrir clientes.*

### Paso B: Arrancar el Cliente
1. Ejecuta la aplicación del Cliente (`ClienteTcpImc`).
2. Verás una ventana llamada **"CLIENTE IMC"**.
3. En la pestaña **"CONEXION"**, asegúrate de que la IP dice `localhost` (si pruebas en la misma PC) y el puerto `9007`.
4. Haz clic en **"Conectar"**. El estado cambiará a color verde ("Conectado").
5. Si revisas la ventana del Servidor, verás que registró una nueva conexión de cliente.

### Paso C: Realizar el Cálculo
1. En la ventana del Cliente, ve a la pestaña **"CALCULAR IMC"**.
2. Ingresa un **PESO** (en kilogramos, por ejemplo `81.0` o `75.5`).
3. Ingresa una **ALTURA** (en metros, por ejemplo `1.70` o `1.85`).
4. Haz clic en **"CALCULAR"**.
5. Inmediatamente el cliente enviará los datos, el servidor los procesará y el cliente mostrará tu IMC exacto junto a un mensaje médico (ej. `"Estas bien de peso"` o `"Debes bajar un poco de peso"`).

## 3. ¿Qué pasa si algo falla?
- **El botón Calcular no hace nada o da error:** Verifica que hayas presionado "Conectar" primero en el cliente.
- **El cliente dice "Falla en la conexión":** Asegúrate de haber presionado "INICIAR" en el Servidor antes de conectar el cliente.
- **Errores de tipeo:** Java espera los decimales con punto o coma dependiendo del idioma de tu sistema (ej. intenta usar `1.70` si `1,70` falla).
