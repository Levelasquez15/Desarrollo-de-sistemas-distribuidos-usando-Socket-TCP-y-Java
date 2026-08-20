# Convenciones de Desarrollo

Basado en la guía de desarrollo proporcionada, se establecen las siguientes convenciones para el proyecto:

## Herramientas y Entorno
- **Lenguaje:** Java (JDK 8).
- **IDE:** Apache NetBeans (versión 12.2 o similar).
- **Interfaces Gráficas:** Java Swing (uso del diseñador visual `JFrame Form`).

## Estructura y Nomenclatura de Paquetes
Se utiliza una estructura de paquetes basada en el dominio y responsabilidades de las clases:
- `imc.modelo`: Contiene las clases de dominio y lógica de negocio (ej. `CalculoImc`).
- `imc.servidor`: Contiene las clases relacionadas con la gestión de conexiones de red del servidor (ej. `ServidorTcp`, `SubProcesoCliente`).
- `imc.cliente`: Contiene las clases principales de ejecución para la aplicación cliente.
- `imc.vistas` / `imc.cliente.vistas`: Contiene las interfaces gráficas (`VentanaPrincipal`).

## Nomenclatura de Código
- **Clases:** Se utiliza `PascalCase` (ej. `CalculoImc`, `SubProcesoCliente`, `VentanaPrincipal`).
- **Variables y Atributos:** Se utiliza `camelCase` (ej. `listaDeClientes`, `hiloResponde`, `peso`, `altura`).
- **Componentes Gráficos (Swing):**
  - Botones: Prefijo `btn` (ej. `btnIniciar`, `btnLimpiar`).
  - Campos de Texto: Prefijo `campo` (ej. `campoIP`, `campoPuerto`, `campoPeso`).
  - Etiquetas Dinámicas: Prefijo `txt` (ej. `txtEstado`, `txtResultado`, `txtMensaje`).
  - Áreas de Texto (Log): `cajaLog`.
  - Etiquetas Estáticas: `jLabel1`, `jLabel2`, etc.

## Estilo de Código
- Los métodos autogenerados por el diseñador visual de NetBeans para el manejo de eventos utilizan el formato `[nombreComponente]ActionPerformed`.
- Las variables de los componentes gráficos se declaran al final de la clase de la vista (comportamiento por defecto de NetBeans).
