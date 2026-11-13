# ADR 0001: Selección de Modelo y Proveedor de IA

**Estado:** Aceptado
**Fecha:** 2026-11-13
**Quién decide:** Alex Cubero, Arquitecto de Software

## Contexto
En sistemas de salud y atención al público, delegar decisiones críticas a algoritmos automatizados conlleva altos riesgos éticos, médicos y legales. Es necesario delimitar exactamente qué puede hacer el asistente de IA y dónde interviene obligatoriamente un profesional humano.

## Decisión
Se establece como regla arquitectónica inquebrantable que **la Inteligencia Artificial únicamente extrae, resume y orienta; nunca diagnostica, prescribe medicamentos, ordena prioridades clínicas de urgencia ni descarta o niega atención médica a un paciente de forma autónoma.**

## Alternativas descartadas
* **Delegar el triaje y asignación de prioridad clínica de forma 100% automática por el modelo:** Descartado por el alto riesgo legal de diagnósticos erróneos y la violación de normativas éticas de salud sobre supervisión médica obligatoria.

## Consecuencias

* **Positivas:** 
  * Se elimina el riesgo de negligencia médica automatizada o sesgos algorítmicos que perjudiquen a poblaciones vulnerables.
  * La responsabilidad clínica y legal permanece siempre en manos de un médico colegiado, cumpliendo con los estándares normativos vigentes.
* **Negativas:** 
  * El flujo de atención requiere obligatoriamente la validación humana antes de emitir cualquier criterio médico definitivo, lo que impide automatizar al 100% la resolución de consultas.

## Cómo se verifica
* Mediante revisión de código de las restricciones del prompt del sistema, validación de las reglas de negocio en los componentes de interfaz que bloquean diagnósticos y auditorías periódicas de las conversaciones almacenadas.
