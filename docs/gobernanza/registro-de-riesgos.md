# Registro de Riesgos y Mitigaciones - Plataforma de Telemedicina con IA

Este documento detalla los principales riesgos tecnológicos, éticos y normativos identificados en el desarrollo y operación de la plataforma, junto con las medidas de mitigación implementadas para prevenirlos.

## Matriz de Evaluación y Mitigación de Riesgos

| ID | Riesgo Identificado | Categoría | Probabilidad | Impacto | Quién sale afectado | Mitigación Implementada | Estado |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **R01** | **Inyección de Prompts maliciosos:** Un usuario intenta ocultar instrucciones en los síntomas para saltar restricciones. | Seguridad (OWASP LLM01) | Media | Alto | Pacientes y Servidor | Separación estricta de instrucciones del sistema, validación con esquemas tipados y sin privilegios de ejecución. | Mitigado |
| **R02** | **Fuga de datos personales en Logs:** Exposición de correos, teléfonos o expedientes en herramientas de monitoreo (Sentry). | Privacidad (Ley 8968) | Baja | Alto | Usuarios del sistema | Capa automática de sanitización que reemplaza PII por etiquetas genéricas (`[email]`, `[phone]`, `[uuid]`). | Mitigado |
| **R03** | **Alucinación o diagnóstico erróneo:** La IA genera una respuesta interpretada como diagnóstico médico definitivo o receta. | Ético y Legal | Media | Crítico | Pacientes | Prohibición absoluta en ADR 0002, disclaimer obligatorio en el chat y validación humana requerida. | Mitigado |
| **R04** | **Comportamiento no autorizado de Agentes:** Un flujo ejecuta acciones destructivas en base de datos o envíos masivos. | Operativo | Baja | Medio | Base de datos | Prohibición de borrado permanente y principio de confirmación humana obligatoria para acciones críticas. | Mitigado |

## Conclusiones del Monitoreo
Este registro se revisa de forma iterativa en cada ciclo de desarrollo del proyecto para asegurar que los riesgos emergentes asociados al uso de inteligencia generativa y gestión de datos queden cubiertos por controles técnicos y políticas escritas.
