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

## 🛡️ Tabla STRIDE utilizada

| ID | Componente / Activo | Tipo STRIDE | Descripción de la Amenaza | Escenario de Ataque | Impacto | Probabilidad | Nivel de Riesgo | Controles de Seguridad Existentes | Mitigación Recomendada | Responsable | Estado |
|----|----------------------|-------------|----------------------------|---------------------|---------|--------------|------------------|-----------------------------------|------------------------|-------------|--------|
| T1 | Autenticación del estudiante y sesión de compra | Spoofing | Un atacante suplanta la identidad de un estudiante para comprar o activar una suscripción ajena | Uso de credenciales robadas o reutilizadas para iniciar sesión y completar el flujo de pago | Acceso no autorizado a cursos, certificados y datos personales | Alta | Alto | Inicio de sesión con usuario y contraseña, cifrado TLS | Implementar MFA, detección de inicios de sesión anómalos y políticas de contraseñas robustas | Equipo de Seguridad | Pendiente |
| T2 | Solicitud de pago y confirmación de la pasarela | Tampering | Alteración de parámetros críticos del pago o del estado de la suscripción | Manipulación del monto, plan o respuesta del webhook para registrar una suscripción como pagada sin una transacción válida | Fraude financiero, pérdida de ingresos y activación indebida de beneficios | Alta | Crítico | HTTPS, integración por API con tercero y validaciones funcionales básicas | Firmar y validar webhooks, recalcular montos en servidor y verificar idempotencia y referencias de transacción | Equipo Backend | Pendiente |
| T3 | Registro de transacciones y auditoría de suscripciones | Repudiation | Un usuario o administrador niega haber ejecutado una compra, reverso o activación manual | La plataforma no conserva trazabilidad suficiente de quién aprobó el cambio, desde qué origen y con qué evidencia | Conflictos operativos, imposibilidad de auditoría y disputas con clientes o pasarela | Media | Medio | Logs de aplicación y registros básicos de pago | Centralizar auditoría, sellar eventos críticos y conservar evidencia de cambios con usuario, fecha, IP y transacción asociada | DevOps / Seguridad | Pendiente |
| T4 | Base de datos de suscripciones, datos personales y notas asociadas a la cuenta | Information Disclosure | Exposición de información personal, historial académico o referencias de pago | Un endpoint de suscripción devuelve más datos de los necesarios o un rol sin autorización consulta información sensible | Incumplimiento de privacidad, fuga de datos y afectación reputacional y legal | Alta | Alto | Control de acceso básico por sesión y uso de TLS | Aplicar RBAC estricto, minimización de datos en respuestas, cifrado en reposo y tokenización de datos de pago | Arquitectura / Backend | Pendiente |
| T5 | API de pagos y servicio de activación de acceso | Denial of Service | Saturación del flujo de pago o de confirmación que impide procesar suscripciones | Envío masivo de solicitudes al checkout o a la recepción de webhooks para bloquear la activación de cursos | Indisponibilidad del servicio, fallas en compras legítimas y afectación de continuidad del negocio | Media | Alto | Rate limiting básico y capacidad estándar de infraestructura | Implementar protección anti-DDoS, colas para procesamiento asíncrono, reintentos controlados y monitoreo con alertas | Infraestructura | Pendiente |
| T6 | Módulo de gestión de suscripciones y asignación de roles | Elevation of Privilege | Un usuario obtiene permisos de estudiante premium, docente o administrador sin autorización | Modificación de tokens, parámetros o llamadas internas para cambiar el rol o el estado de la suscripción | Acceso a contenido restringido, cambios sobre certificados y exposición de funciones administrativas | Media | Crítico | Separación básica de roles en la aplicación | Validar autorización del lado servidor en cada operación, usar claims firmados y revisar periódicamente privilegios y cambios de rol | Equipo de Seguridad / Backend | Pendiente |

## 🔁 Tareas definidas para complementar el taller

| Tarea asignada | Responsable | Fecha estimada |
|----------------|-------------|----------------|
| Diligenciar la tabla STRIDE en la plantilla final de Excel | Esteban Fernando Forero Montejo | 14/03/2026 |
| Revisar amenazas, impactos y redacción del análisis | Carlos David Cruz Pavas | 14/03/2026 |
| Validar mitigaciones y consistencia con el caso EdukIT | Juan Felipe Cepeda Uribe | 14/03/2026 |

---

_Este documento resume el trabajo colaborativo realizado durante la sesión del Taller 5 en el curso de Arquitectura Empresarial - Universidad de La Sabana._
