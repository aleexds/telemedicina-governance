# ADR 0001: Selección de Modelo y Proveedor de IA

**Estado:** Aceptado
**Fecha:** 2026-11-13
**Quién decide:** Alex Cubero, Arquitecto de Software

## Contexto
La gestión de expedientes médicos, citas e información personal de pacientes exige controles estrictos de ubicación, acceso y protección frente a filtraciones de seguridad, en alineación con la Ley 8968. Es crítico definir dónde residen los datos, quién puede leerlos y cómo se protegen ante servicios externos. El procesamiento del dato sensible de **Historial de síntomas y pre-diagnóstico** es estrictamente necesario para que el asistente de IA pueda estructurar la pre-consulta y orientar al paciente hacia la especialidad médica correcta antes de la cita.

## Decisión
Se establece que **todos los datos personales y clínicos residirán exclusivamente en una base de datos relacional cifrada con control de acceso estricto a nivel de fila**, aplicando anonimización obligatoria antes de enviar cualquier fragmento de texto a APIs de terceros o sistemas de monitoreo.

## Alternativas descartadas
* **Almacenamiento de datos en bases de datos NoSQL sin RLS ni cifrado nativo:** Descartado por la dificultad extrema de asegurar un control de acceso granular por fila para expedientes médicos sensibles.

## Consecuencias

* **Positivas:** 
  * Se previene la exposición accidental de datos sensibles ante fallos de configuración o accesos no autorizados.
  * Se minimiza el impacto en caso de brechas de seguridad en servicios externos de monitoreo, ya que dichos sistemas nunca reciben PII.
* **Negativas:** 
  * Aumenta ligeramente la complejidad durante el desarrollo, ya que cada nueva tabla requiere configurar políticas de seguridad RLS.

## Cómo se verifica
* Mediante pruebas automatizadas de seguridad sobre las políticas RLS en las migraciones de base de datos, inspección de tráfico de red hacia APIs externas para comprobar el enmascaramiento de PII y revisión de configuraciones de cifrado en reposo.
