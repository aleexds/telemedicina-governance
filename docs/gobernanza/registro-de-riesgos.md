# Registro de Riesgos y Mitigaciones - Plataforma de Telemedicina con IA

Este documento detalla los principales riesgos tecnológicos, éticos y normativos identificados en el desarrollo y operación de la plataforma, junto con las medidas de mitigación implementadas para prevenirlos.

## Matriz de Evaluación y Mitigación de Riesgos

| ID | Riesgo Identificado | Categoría | Impacto | Mitigación Implementada en el Proyecto |
| :--- | :--- | :--- | :--- | :--- |
| **R01** | **Inyección de Prompts maliciosos:** Un usuario malintencionado intenta ocultar instrucciones en el texto de síntomas para forzar al modelo de IA a revelar datos sensibles o saltarse restricciones. | Seguridad (OWASP LLM01) | Alto | • Separación estricta de las instrucciones del sistema y los datos ingresados.<br>• Validación estricta de la estructura de entrada y salida de los datos con esquemas tipados.<br>• El modelo no cuenta con privilegios ni herramientas de ejecución en el servidor. |
| **R02** | **Fuga de datos personales en Logs de Errores:** Exposición de correos, números de teléfono o expedientes clínicos en herramientas externas de monitoreo (ej. Sentry). | Privacidad (Ley 8968) | Alto | • Capa automática de interceptación de errores que reemplaza correos, teléfonos y UUIDs por etiquetas genéricas (`[email]`, `[phone]`, `[uuid]`) antes de enviar cualquier registro al exterior. |
| **R03** | **Alucinación o diagnóstico clínico automatizado erróneo:** El asistente de IA genera una respuesta que el paciente interpreta como un diagnóstico médico definitivo o una prescripción. | Ético y Legal | Crítico | • Prohibición absoluta de emitir diagnósticos o puntajes en el ADR 0002.<br>• Inclusión obligatoria de mensajes de descargo de responsabilidad ("Disclaimer") en la interfaz del chat.<br>• Validación humana obligatoria antes de registrar cualquier criterio clínico. |
| **R04** | **Comportamiento no autorizado de Agentes:** Un flujo automatizado o agente ejecuta acciones destructivas en la base de datos o envía notificaciones masivas sin supervisión. | Operativo / Arquitectura | Medio | • El agente tiene prohibido borrar archivos o bases de datos (lo obsoleto va a una papelera de revisión humana manual).<br>• Principio de "ante la duda, no actuar": el sistema requiere confirmación humana para cualquier acción de alto impacto. |

## Conclusiones del Monitoreo
Este registro se revisa de forma iterativa en cada ciclo de desarrollo del proyecto para asegurar que los riesgos emergentes asociados al uso de inteligencia generative y gestión de datos queden cubiertos por controles técnicos y políticas escritas.
