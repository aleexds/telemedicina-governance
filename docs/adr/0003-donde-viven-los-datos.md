# ADR 0003: Arquitectura de Almacenamiento, Seguridad y Flujo de Datos

* **Estado:** Aceptado
* **Fecha:** 2026-11-13
* **Contexto:** La gestión de expedientes médicos, citas e información personal de pacientes en Costa Rica exige controles estrictos de ubicación, acceso y protección frente a filtraciones de seguridad, en alineación con la Ley 8968 y sus reformas de ciberseguridad. Es crítico definir dónde residen los datos, quién puede leerlos o modificarlos y cómo se protegen al interactuar con servicios externos.

## Decisión
Se establece que **todos los datos personales y clínicos residirán exclusivamente en una base de datos relacional cifrada con control de acceso estricto a nivel de fila**, aplicando anonimización obligatoria antes de enviar cualquier fragmento de texto a APIs de terceros o sistemas de monitoreo.

## Reglas Técnicas de Protección y Acceso

* **Control de Acceso Granular (RLS y Roles):** Toda tabla nueva creada en la base de datos debe incluir en su misma migración la activación de `Row Level Security` (RLS) y permisos explícitos (`GRANT`) por rol[cite: 14]. Un paciente únicamente puede leer y editar sus propios registros, mientras que un médico solo tiene acceso de lectura a los expedientes de los pacientes que tienen una cita confirmada con él.
* **Cifrado en Reposo y en Tránsito:** Toda comunicación entre el cliente, el servidor y la base de datos utiliza cifrado TLS 1.3 en tránsito y cifrado AES-256 en reposo.
* **Anonimización hacia Servicios de Terceros:** Antes de enviar una consulta al proveedor de IA (Anthropic) o registrar un evento en herramientas de monitoreo de errores (como Sentry), una capa intermedia de limpieza reemplaza automáticamente cualquier dato identificable (nombres, cédulas, correos y teléfonos) por marcadores genéricos (`[uuid]`, `[email]`, `[phone]`)[cite: 19].
* **Privacidad por Defecto:** Todos los perfiles de usuario y resúmenes clínicos se crean con visibilidad estrictamente privada por defecto[cite: 19], requiriendo el consentimiento explícito e informado del paciente[cite: 10] antes de compartir cualquier dato con un especialista.

## Consecuencias

* **Positivas:** 
  * Se previene la exposición accidental de datos sensibles ante fallos de configuración o accesos no autorizados (bloqueando consultas sin permisos explícitos desde el motor de base de datos)[cite: 14].
  * Se minimiza el impacto en caso de brechas de seguridad en servicios externos de monitoreo o análisis, ya que dichos sistemas nunca reciben información personalmente identificable (PII)[cite: 19].
* **Negativas:** 
  * Aumenta ligeramente la complejidad durante el desarrollo y pruebas, ya que cada nueva tabla o consulta requiere configurar y validar sus políticas de seguridad RLS antes de desplegarse[cite: 14].
