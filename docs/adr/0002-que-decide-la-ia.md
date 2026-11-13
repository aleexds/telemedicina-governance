# ADR 0002: Alcance de Decisiones y Límites de Autonomía de la IA

* **Estado:** Aceptado
* **Fecha:** 2026-11-13
* **Contexto:** En sistemas de salud y atención al público, delegar decisiones críticas a algoritmos automatizados conlleva altos riesgos éticos, médicos y legales (como se ha evidenciado en casos internacionales de discriminación o diagnósticos erróneos automatizados). Es necesario delimitar exactamente qué puede hacer el asistente de IA y dónde interviene obligatoriamente un profesional humano.

## Decisión
Se establece como regla arquitectónica inquebrantable que **la Inteligencia Artificial únicamente extrae, resume y orienta; nunca diagnostica, prescribe medicamentos, ordena prioridades clínicas de urgencia ni descarta o niega atención médica a un paciente de forma autónoma.**

## Reglas de Operación y Supervisión Humana (Human-in-the-Loop)

* **Rol de Asistencia y Extracción:** El modelo de lenguaje se limita a conversar con el paciente para recopilar sus síntomas reportados, estructurar un resumen clínico preliminar y sugerir especialidades médicas disponibles para agendar una cita.
* **Prohibición de Puntuación y Descarte:** El sistema tiene estrictamente prohibido asignar puntajes de "riesgo", clasificar pacientes por nivel de prioridad de atención o bloquear el acceso a una consulta médica basándose en el perfil sociodemográfico o historial del usuario.
* **Confirmación Explícita:** Ningún resumen clínico o recomendación de especialidad se guarda en el expediente médico oficial ni se envía a un doctor sin que el paciente haya revisado y confirmado previamente que la información extraída es correcta.
* **Escalamiento Obligatorio a Humanos:** Ante la detección de palabras clave asociadas a emergencias médicas graves, distrés psicológico agudo o consultas legales/administrativas complejas, el flujo automatizado detiene las sugerencias y deriva de inmediato al paciente hacia una línea de atención humana directa o servicios de emergencia.

## Consecuencias

* **Positivas:** 
  * Se elimina el riesgo de negligencia médica automatizada o sesgos algorítmicos que perjudiquen a poblaciones vulnerables.
  * La responsabilidad clínica y legal permanece siempre en manos de un médico colegiado con nombre y apellido, cumpliendo con los estándares éticos y normativos vigentes.
* **Negativas:** 
  * El flujo de atención requiere obligatoriamente la validación humana antes de emitir cualquier criterio médico definitivo, lo que impide automatizar al 100% la resolución de consultas.
