# Inventario de datos

No se puede gobernar lo que no se sabe que se tiene. Una fila por cada dato que el sistema guarda, recibe o envía a un tercero, incluido el proveedor del modelo de IA.

| Dato | ¿Personal? | Categoría (Ley 8968, art. 9) | De dónde viene | Dónde se guarda | ¿Sale a un tercero? ¿A quién? | Cuánto se conserva | Quién puede verlo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Nombre completo y cédula | Sí | Acceso restringido | Formulario de registro del paciente | Supabase (tabla `users`) | No | Hasta solicitud de supresión (Derechos ARCO) | El propio usuario y administradores |
| Historial de síntomas y pre-diagnóstico | Sí | Salud (Datos Sensibles) | Ingreso directo por el paciente en el chat | Supabase (tabla `medical_records`) | Sí: Proveedor de IA (Anthropic), solo para extracción y resumen clínico (anonimizado) | Tiempo estipulado por normativa de salud | El paciente y el médico asignado |
| Correo electrónico y teléfono | Sí | Acceso restringido | Perfil de usuario | Supabase (tabla `users`) | Sí: Pasarela de notificaciones (solo para avisos de citas) | 1 año tras inactividad de cuenta | El usuario |
| Coordenadas de conexión / Logs de error | No | No aplica | Generado automáticamente por el servidor | Servidores de Monitoreo (Sentry) | Sí: Sentry (con enmascaramiento previo de PII) | 90 días | Equipo de desarrollo |

<!--
Categorías de la Ley 8968 (art. 9):
- Sensibles: origen racial o étnico, opiniones políticas, convicciones religiosas, salud,
  vida y orientación sexual; la definición del art. 3 incluye la condición socioeconómica
  y la información biomédica o genética. Si aparece uno, expliquen en un ADR por qué lo necesitan.
- Acceso restringido: de interés solo para la persona o la administración (correo, teléfono, dirección).
- Acceso irrestricto: los que constan en bases públicas de acceso general.
- Crediticios: comportamiento crediticio de la persona.
-->

## Lo que NO recolectamos

- Datos de salud mental profunda: decidimos no requerirlos ni almacenarlos en la pre-consulta para evitar riesgos innecesarios de manejo de datos altamente sensibles no indispensables para la cita general.
- Biometría avanzada (huella o reconocimiento facial): no la necesitamos porque la autenticación se realiza mediante credenciales tradicionales seguras de usuario y contraseña.
