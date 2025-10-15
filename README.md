# Pruebas automatizadas con Cypress
## 1. Visión general del proyecto
Esta suite de pruebas automatizadas fue diseñada para verificar dos funcionalidades críticas de la aplicación: el flujo de inicio de sesión (Login) y el flujo de restablecimiento de contraseña. El objetivo principal es asegurar la correcta gestión de usuarios y la seguridad del acceso.

El código de automatización se implementó con Cypress y se utilizó ChatGPT-5 como herramienta de apoyo para la generación y estructuración de los scripts.

## 2 . Requisitos y configuración
Para poder ejecutar estas pruebas, es necesario tener instalado lo siguiente:

Node.js: La versión 12 o superior.

Cypress: Se instalará como dependencia del proyecto.

Para la configuración inicial, navega al directorio del proyecto y ejecuta el siguiente comando en tu terminal para instalar todas las dependencias:

npm install

## 3. Funcionalidades bajo prueba
### A. Login
Verifica que solo los usuarios con credenciales válidas y verificadas puedan acceder al sistema, bloqueando cualquier intento de acceso indebido.

* Flujo principal:
CP001: Inicio de sesión exitoso con usuario y contraseña correctos. El sistema redirige a la URL principal, confirma el acceso y cierra sesión.

* Casos alternativos:
CP002: Usuario no verificado.

CP003, CP004, CP006: Datos de email o contraseña incorrectos.

CP005, CP007, CP008: Campos de email o contraseña vacíos.

* Test exploratorio: Usuario no verificado + contraseña vacía.

### B. Restablecimiento de contraseña
Asegura que los usuarios puedan recuperar el acceso a sus cuentas de forma segura en caso de haber olvidado su contraseña.

* Flujo principal:
CP001 - CP004: Restablecimiento de contraseña exitoso de extremo a extremo (navegación, envío de correo, recepción del link y cambio de contraseña).

* Casos alternativos:

CP005 - CP007: Emails inválidos, inexistentes o no verificados.

CP009: Intento de usar una contraseña nueva inválida.

CP010: Contraseña nueva y confirmación no coinciden.

Consideraciones sobre la verificación por correo

Para validar la recepción del correo de restablecimiento de contraseña, fue necesario utilizar una cuenta real de Gmail configurada con verificación en dos pasos y una contraseña de aplicación.
Esto permitió que Cypress pudiera conectarse directamente a la bandeja de entrada mediante IMAP y leer el mensaje de restablecimiento enviado por el sistema bajo prueba.

### ¿Por qué se usó una cuenta de Gmail?

Durante el desarrollo, se evaluaron varios servicios de correo temporal (como GuerrillaMail, Mail7 y otros) para realizar la verificación automática del enlace de restablecimiento.
Sin embargo, se presentaron las siguientes limitaciones:

Los servicios gratuitos no permitían crear cuentas persistentes ni recibir correos desde dominios externos seguros.

Algunas APIs de correos temporales habían sido restringidas o requerían suscripción de pago para permitir consultas automáticas.

Los dominios de email temporal eran bloqueados por el servidor de la aplicación bajo prueba, impidiendo que los correos de restablecimiento llegaran correctamente.

Debido a esto, se optó por usar una cuenta de Gmail de prueba, creada específicamente para este flujo.
Gmail ofrece soporte completo para autenticación IMAP segura, lo cual permitió integrar la verificación real del correo sin depender de servicios inestables o bloqueados.

Manejo de credenciales

Para evitar exponer información sensible, se usó un archivo de entorno (cypress.env.json) donde se almacenan las credenciales:

{
  "GMAIL_ADDRESS": "correo_de_prueba@gmail.com",
  "GMAIL_APP_PASSWORD": "clave_de_16_caracteres"
}


En el repositorio público, estos valores se reemplazan por ejemplos ficticios.
El evaluador puede agregar sus propias credenciales de Gmail de prueba para ejecutar el flujo completo de forma segura.

### Seguridad y buenas prácticas

La cuenta utilizada no tiene datos personales ni acceso a otros servicios de Google.

La clave de aplicación puede revocarse en cualquier momento desde la configuración de seguridad de Gmail.

Se recomienda nunca incluir credenciales reales en repositorios públicos y usar variables de entorno o cuentas temporales de prueba.

## 4. Objetivos de las pruebas
La suite de pruebas busca cumplir con los siguientes objetivos generales:

Validar la seguridad: Asegurar que los intentos de acceso y los cambios de contraseña con datos incorrectos o incompletos sean bloqueados de forma segura.

Confirmar la experiencia de usuario: Verificar que los mensajes de error sean claros, precisos y coherentes en todas las interacciones.

Verificar la funcionalidad: Comprobar que los flujos de login y restablecimiento funcionen correctamente de extremo a extremo.

Garantizar la consistencia: Validar el comportamiento del sistema tanto en escenarios válidos (camino feliz) como en escenarios de error (casos alternativos).

## 5. Estructura del proyecto
El proyecto de automatización sigue la siguiente estructura de directorios:

cypress/e2e/: Contiene los archivos de los casos de prueba (tests).

cypress/fixtures/: Almacena los datos de prueba (test data), como las credenciales de usuarios.

cypress/support/: Incluye comandos personalizados y constantes que se utilizan a lo largo de las pruebas.

## 6. Instrucciones de ejecución
Para correr los tests, asegúrate de tener las dependencias instaladas y luego ejecuta uno de los siguientes comandos en la terminal:

npx cypress open: Este comando abre la interfaz de usuario de Cypress, donde puedes ver y ejecutar los tests de forma interactiva. Es ideal para el desarrollo y la depuración.

npx cypress run: Este comando ejecuta todos los tests en la línea de comandos de forma automática (sin abrir la interfaz gráfica). Es útil para la integración continua (CI) o para ejecuciones rápidas y sin supervisión.
