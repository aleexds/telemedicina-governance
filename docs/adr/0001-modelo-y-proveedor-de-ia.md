# ADR 0001: Selección de Modelo y Proveedor de IA

**Estado:** Aceptado
**Fecha:** 2026-11-13
**Quién decide:** Alex Cubero, Arquitecto de Software

## Contexto
La plataforma de telemedicina requiere integrar un asistente conversacional automatizado que opere como triaje inicial, procesando las descripciones de síntomas de los pacientes, estructurando historiales previos y ayudando a direccionar la consulta hacia la especialidad médica adecuada de forma rápida, segura y bajo estricto cumplimiento normativo.

## Decisión
Se decide implementar el modelo **Claude 3.5 Sonnet (mediante la API oficial de Anthropic)** como el motor central de Inteligencia Artificial para el procesamiento de lenguaje natural y la asistencia analítica en la plataforma.

## Alternativas descartadas
* **Modelos open-source auto-hospedados (ej. Llama 3 en infraestructura propia):** Descartados en esta fase inicial debido a los elevados costos de aprovisionamiento de hardware con GPUs dedicadas y la complejidad operativa de mantenimiento.
* **APIs de proveedores alternativos sin compromisos explícitos de privacidad encriptada:** Descartadas por el riesgo legal y técnico de exponer información sensible de pacientes a servidores de terceros sin garantías contractuales robustas.

## Consecuencias

* **Positivas:** 
  * Se obtiene un asistente sumamente preciso que reduce el margen de error y alucinaciones en respuestas críticas.
  * Se asegura un marco legal transparente de tratamiento de datos con el proveedor tecnológico.
* **Negativas:** 
  * Se genera una dependencia tecnológica directa de la infraestructura de Anthropic.
  * Los costos de operación son variables y dependen estrictamente del volumen de tokens procesados, lo que obliga a implementar límites estrictos en la longitud máxima de los historiales de chat.

## Cómo se verifica
* Mediante auditoría de código del módulo de integración con la API, verificación de los términos de servicio/cero retención de datos del proveedor y pruebas de integración de los mensajes de chat.
