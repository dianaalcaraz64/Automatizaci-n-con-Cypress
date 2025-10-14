# Automatizacion-con-Cypress
Este es un pequeño proyecto donde se automatiza el formulario de login y restablecimiento de contraseña de la aplicación Tiketazo.

##1. Visión general del proyecto
Esta suite de pruebas automatizadas fue diseñada para validar la funcionalidad integral de la aplicación Ticketazo desde la perspectiva de diferentes usuarios. El objetivo principal es asegurar la estabilidad, seguridad y calidad del sistema en sus flujos clave, desde el registro de usuarios hasta la gestión y compra de eventos.

El código de automatización fue implementado con Cypress y utiliza Node.js y npm como base.

##2. Funcionalidades bajo prueba
Aquí se documentan las principales funcionalidades de la aplicación que han sido cubiertas por las pruebas de automatización:

###Inicio de sesión (Login): Validaciones para acceso de usuarios con credenciales válidas y manejo de errores para credenciales inválidas o usuarios no verificados.

###Restablecimiento de contraseña: Verificación del flujo completo de recuperación de contraseña, incluyendo el envío de correo de confirmación y el cambio de contraseña.

##3. Tipos de usuario
Las pruebas fueron diseñadas para validar el comportamiento del sistema desde la perspectiva de tres roles principales:

###Super Administrador: Gestor del sistema con acceso total.

###Usuario Cliente: Usuario común que consume contenido y compra entradas.

###Usuario Creador de Eventos: Usuario que crea y gestiona eventos para su publicación.

##4. Requisitos y configuración
Para poder ejecutar estas pruebas, es necesario tener instalado lo siguiente:

Node.js: La versión 12 o superior.

Cypress: Se instalará como dependencia del proyecto.

Para la configuración inicial, navega al directorio del proyecto y ejecuta el siguiente comando en tu terminal para instalar todas las dependencias:

npm install

##5. Instrucciones de ejecución
Para correr los tests, asegúrate de tener las dependencias instaladas y luego ejecuta uno de los siguientes comandos en la terminal:

npx cypress open: Este comando abre la interfaz de usuario de Cypress, donde puedes ver y ejecutar los tests de forma interactiva.

npx cypress run: Este comando ejecuta todos los tests en la línea de comandos de forma automática.
