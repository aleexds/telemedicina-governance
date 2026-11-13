# Inventario de Datos - Plataforma de Telemedicina con IA

Este documento registra los flujos, categorías, almacenamiento y ciclo de vida de los datos tratados en la plataforma de telemedicina, asegurando el cumplimiento de la privacidad y la Ley 8968 de protección de datos personales.

## 1. Categorías de Datos Recolectados

| Categoría de Dato | Descripción / Ejemplos | Nivel de Sensibilidad | Origen y Recolección |
| :--- | :--- | :--- | :--- |
| **Datos de Salud y Clínicos** | Historial médico, síntomas reportados, diagnósticos preliminares del asistente de IA y recetas. | **Alto (Sensible)** | Ingreso directo por el paciente o interacción con el chat médico. |
| **Datos de Identificación** | Nombre completo, número de cédula o documento de identidad del paciente y médicos. | **Alto** | Formulario de registro de cuenta. |
| **Datos de Contacto** | Correo electrónico, número de teléfono móvil y dirección física opcional. | **Medio** | Datos provistos por el usuario al registrarse. |
| **Datos de Auditoría y Logs** | Registros de acceso al sistema, marcas de tiempo y trazas de errores del software. | **Bajo (No personal)** | Generados automáticamente por el servidor y herramientas de monitoreo. |

## 2. Almacenamiento, Flujo y Destino

* **Base de Datos Principal:** Todos los datos estructurados (identificación, perfiles y citas) se almacenan en servidores cifrados en reposo y en tránsito.
* **Procesamiento de IA:** Las consultas sobre síntomas viajan a la API del modelo de lenguaje de forma encriptada, utilizando únicamente identificadores anónimos (`[uuid]`) para evitar exponer los datos reales de los pacientes a terceros.
* **Manejo de Errores (Sentry/Logs):** Los registros de depuración y errores filtran automáticamente cualquier rastro de correos, teléfonos o nombres, reemplazándolos con etiquetas genéricas (`[email]`, `[phone]`) antes de salir del servidor.

## 3. Retención, Supresión y Derechos ARCO

* **Plazos de Retención:** Los registros clínicos se almacenan por el tiempo estipulado por la normativa de salud aplicable. Los registros de actividad y logs se purgan automáticamente cada 90 días.
* **Derechos ARCO (Acceso, Rectificación, Cancelación y Oposición):** El sistema cuenta con flujos definidos para que los usuarios puedan solicitar la exportación de sus datos personales o la eliminación total de su cuenta e historial clínico cuando lo requieran.
