# Registro de Riesgos y Mitigaciones - Plataforma de Telemedicina con IA

Este documento detalla los principales riesgos tecnológicos, éticos y normativos identificados en el desarrollo y operación de la plataforma, junto con las medidas de mitigación implementadas para prevenirlos.

## Matriz de Evaluación y Mitigación de Riesgos

| ID | Riesgo Identificado | Categoría | Probabilidad | Impacto | Quién sale afectado | Mitigación Implementada | Estado |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **R01** | Inyección de Prompts maliciosos | Seguridad (OWASP LLM01) | Media | A | Pacientes y Servidor | Separación estricta de instrucciones del sistema y validación de datos. | Hecho |
| **R02** | Fuga de datos personales en Logs | Privacidad (Ley 8968) | Baja | A | Usuarios del sistema | Capa automática de sanitización y enmascaramiento de PII. | Hecho |
| **R03** | Alucinación o diagnóstico erróneo | Ético y Legal | Media | A | Pacientes | Prohibición absoluta en ADR 0002 y validación humana obligatoria. | Hecho |
| **R04** | Comportamiento no autorizado | Operativo | Baja | M | Base de datos | Principio de confirmación humana para acciones críticas. | Hecho |

## Conclusiones del Monitoreo
Este registro se revisa de forma iterativa en cada ciclo de desarrollo del proyecto para asegurar que los riesgos emergentes asociados al uso de inteligencia generativa y gestión de datos queden cubiertos por controles técnicos y políticas escritas.
