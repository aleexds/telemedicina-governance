# Inventario de Datos - Plataforma de Telemedicina con IA

Este documento registra los flujos, categorías, almacenamiento y ciclo de vida de los datos tratados en la plataforma de telemedicina, asegurando el cumplimiento de la privacidad y la Ley 8968 de protección de datos personales.

## 1. Inventario y Categorías de Datos

| Dato | ¿Personal? | Categoría (Ley 8968, art. 9) | De dónde viene | Dónde se guarda | ¿Sale a un tercero? ¿A quién? | Cuánto se conserva | Quién puede verlo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Nombre completo y cédula | Sí | Acceso restringido | Formulario de registro del paciente | Supabase (tabla `users`) | No | Hasta solicitud de supresión (Derechos ARCO) | El propio usuario y administradores |
| Historial de síntomas y pre-diagnóstico | Sí | Salud (Datos Sensibles) | Ingreso directo por el paciente en el chat | Supabase (tabla `medical_records`) | Sí: Proveedor de IA (Anthropic), solo para extracción y resumen clínico (anonimizado) | Tiempo estipulado por normativa de salud | El paciente y el médico asignado |
| Correo electrónico y teléfono | Sí | Acceso restringido | Perfil de usuario | Supabase (tabla `users`) | Sí: Pasarela de notificaciones (solo para avisos de citas) | 1 año tras inactividad de cuenta | El usuario |
| Coordenadas de conexión / Logs de error | No | No aplica | Generado automáticamente por el servidor | Servidores de Monitoreo (Sentry) | Sí: Sentry (con enmascaramiento previo de PII) | 90 días | Equipo de desarrollo |

## 2. Almacenamiento, Flujo y Destino

* **Base de Datos Principal:** Todos los datos estructurados (identificación, perfiles y citas) se almacenan en servidores cifrados en reposo y en tránsito.
* **Procesamiento de IA:** Las consultas sobre síntomas viajan a la API del modelo de lenguaje de forma encriptada, utilizando únicamente identificadores anónimos (`[uuid]`) para evitar exponer los datos reales de los pacientes a terceros.
* **Manejo de Errores (Sentry/Logs):** Los registros de depuración y errores filtran automáticamente cualquier rastro de correos, teléfonos o nombres, reemplazándolos con etiquetas genéricas (`[email]`, `[phone]`) antes de salir del servidor.

## 3. Retención, Supresión y Derechos ARCO

* **Plazos de Retención:** Los registros clínicos se almacenan por el tiempo estipulado por la normativa de salud aplicable. Los registros de actividad y logs se purgan automáticamente cada 90 días.
* **Derechos ARCO (Acceso, Rectificación, Cancelación y Oposición):** El sistema cuenta con flujos definidos para que los usuarios puedan solicitar la exportación de sus datos personales o la eliminación total de su cuenta e historial clínico cuando lo requieran.

## Lo que NO recolectamos

- Datos de salud mental profunda: decidimos no requerirlos ni almacenarlos en la pre-consulta para evitar riesgos innecesarios de manejo de datos altamente sensibles no indispensables para la cita general.
- Biometría avanzada (huella o reconocimiento facial): no la necesitamos porque la autenticación se realiza mediante credenciales tradicionales seguras de usuario y contraseña.