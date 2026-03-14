# 🗒️ Registro de Trabajo en Clase - Taller 5

## 📆 Fecha de la sesión
14/03/2026

## 👥 Integrantes presentes
- Carlos David Cruz Pavas (CarlosDaCruz)
- Juan Felipe Cepeda Uribe
- Esteban Fernando Forero Montejo (EstebanForero)

## 🧠 Actividades realizadas en clase

Durante la sesión el equipo analizó el caso de EdukIT y revisó cuáles procesos eran más sensibles desde la perspectiva de seguridad. Se discutieron especialmente tres flujos: acceso de estudiantes a cursos, publicación de contenidos por docentes y procesamiento de pagos con terceros.

Como decisión de modelado, se seleccionó el flujo de **procesamiento de pagos de suscripción y habilitación de acceso a cursos** por ser el que concentra autenticación, datos personales, interacción con un tercero de pagos y cambios sobre privilegios de acceso dentro de la plataforma.

También se acordó aplicar STRIDE sobre ese flujo usando una tabla de amenazas por categoría, identificando:

- activo o componente afectado;
- amenaza principal;
- escenario de ataque;
- impacto para la operación y la información;
- probabilidad y nivel de riesgo;
- controles existentes y mitigaciones recomendadas.

Para el trabajo se usó la plantilla suministrada en Excel como base del análisis y se tomó como referencia el archivo de ejemplo para mantener el mismo formato de diligenciamiento.

Durante la clase se alcanzó a:

- definir el flujo crítico a evaluar;
- identificar los roles involucrados: Estudiante, Administrador, Pasarela de pagos y plataforma EdukIT;
- establecer seis amenazas, una por cada categoría de STRIDE;
- justificar impactos sobre confidencialidad, integridad, disponibilidad y control de acceso.

## 🧩 Boceto inicial del modelo

Se planteó de forma preliminar el siguiente flujo:

1. El estudiante inicia sesión en EdukIT.
2. Selecciona o renueva la suscripción.
3. La plataforma redirige o consume la pasarela de pagos de un tercero.
4. El tercero confirma el resultado del pago a EdukIT.
5. EdukIT actualiza el estado de la suscripción.
6. El sistema habilita el acceso a cursos, certificados y funcionalidades asociadas.

Este flujo se tomó como base para el análisis STRIDE porque cualquier falla en autenticación, validación del pago o asignación de permisos puede afectar información académica, datos personales y acceso a contenidos pagos.

## 🔁 Tareas definidas para complementar el taller

| Tarea asignada | Responsable | Fecha estimada |
|----------------|-------------|----------------|
| Diligenciar la tabla STRIDE en la plantilla final de Excel | Esteban Fernando Forero Montejo | 14/03/2026 |
| Revisar amenazas, impactos y redacción del análisis | Carlos David Cruz Pavas | 14/03/2026 |
| Validar mitigaciones y consistencia con el caso EdukIT | Juan Felipe Cepeda Uribe | 14/03/2026 |

---

_Este documento resume el trabajo colaborativo realizado durante la sesión del Taller 5 en el curso de Arquitectura Empresarial - Universidad de La Sabana._
