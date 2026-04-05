# 🗒️ Registro de Trabajo en Clase - Taller 6

## 📆 Fecha de la sesión
05/04/2026

## 👥 Integrantes presentes
- Carlos David Cruz Pavas
- Juan Felipe Cepeda Uribe
- Esteban Fernando Forero Montejo

## 🧠 Actividades realizadas en clase

Revisamos qué tipo de información procesa la plataforma y por qué su operación exige controles más estrictos por tratar datos personales y datos sensibles de los ciudadanos.

Hablamos principalmente estos puntos:

- Qué datos maneja GobData: identificación, historial clínico, direcciones, certificados y trazabilidad de trámites.
- Qué normas aplican de forma más directa al caso: Ley 1581 de 2012, principios de Habeas Data e ISO/IEC 27001 como referencia para controles de seguridad.
- Qué evidencias deberían existir para considerar que el sistema cumple: consentimiento, control de acceso por roles, auditoría, retención de datos y medidas contra fuga de información.
- Qué hallazgos preliminares se pueden registrar aun sin conocer la implementación técnica exacta del sistema.

Decidimos abordar el checklist por secciones para no mezclar requisitos legales con controles técnicos. La revisión quedó organizada así:

- Consentimiento y tratamiento de datos personales.
- Gestión de acceso y segregación de roles.
- Auditoría y trazabilidad de operaciones.
- Protección de datos sensibles y prevención de fugas.
- Retención, actualización y eliminación de información.

Como parte del trabajo dejamos una evaluación inicial del caso base, con observaciones como estas:

- El sistema debería pedir autorización clara para tratamientos que no estén cubiertos por obligación legal directa del Estado.
- El acceso a información clínica o de identidad no debería estar disponible para cualquier funcionario, sino limitado según funciones.
- Deben existir bitácoras de acceso y cambios sobre los datos para soportar auditoría y seguimiento.
- Hace falta validar políticas de retención y eliminación para evitar conservar datos sensibles por más tiempo del necesario.
- También es importante contemplar controles de cifrado, monitoreo y prevención de fuga de datos en documentos y notificaciones.

La herramienta usada fue el documento base del taller y la plantilla de notas del repositorio inicial.

## 🧩 Boceto inicial del modelo

se realizo una organización inicial del checklist por "dominios" de cumplimiento. se realizo una lista de preguntas guía para revisar:

- qué datos se recolectan,
- bajo qué base legal se tratan,
- quién puede acceder,
- qué eventos quedan auditados,
- cuánto tiempo se conservan,
- y qué controles existen para protegerlos.

Ese esquema nos sirvió como base para diligenciar la revisión del caso durante la clase.

## 🔁 Tareas definidas para complementar el taller

Para cerrar únicamente la parte trabajada en clase, acordamos estas tareas de organización:

| Tarea asignada | Responsable | Fecha estimada |
|----------------|-------------|----------------|
| Ajustar redacción final de las notas del taller 6 | Esteban Fernando Forero Montejo | 05/04/2026 |
| Revisar coherencia de los hallazgos del caso GobData | Juan Felipe Cepeda Uribe | 05/04/2026 |
| Verificar que los criterios estén alineados con Ley 1581 e ISO 27001 | Carlos David Cruz Pavas | 05/04/2026 |

---

_Este documento resume el trabajo colaborativo realizado durante la sesión del Taller 6 del curso de Arquitectura Empresarial en la Universidad de La Sabana._
