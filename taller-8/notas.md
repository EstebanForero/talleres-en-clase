# Registro de Trabajo en Clase - Taller 8

## Fecha de la sesion

Mayo de 2026

## Integrantes presentes

- Carlos David Cruz Pavas
- Juan Felipe Cepeda Uribe
- Esteban Fernando Forero Montejo

## Objetivo de la sesion

Preparar una defensa ejecutiva de la arquitectura final del cliente real. La presentacion debia conectar problema, analisis, solucion, riesgos y decisiones tecnicas en menos de 10 minutos.

## Actividades realizadas

- Se organizo una narrativa de presentacion: problema actual, riesgos del AS-IS, propuesta TO-BE y beneficios.
- Se reviso que las vistas de negocio, informacion, aplicaciones, infraestructura y seguridad fueran coherentes entre si.
- Se discutieron posibles preguntas del comite: costo de hosting, dependencia de Turso, recuperacion, baseline y control del proveedor.
- Se definio que la presentacion final debia defender la decision de usar aplicacion local con sincronizacion online y respaldos documentales.
- Se preparo una matriz de riesgos arquitectonicos para soportar la defensa tecnica.

## Narrativa propuesta para la defensa

1. El proceso actual funciona, pero depende demasiado de Excel, revision manual y conocimiento tacito.
2. El riesgo central es perder trazabilidad o entregar al proveedor una version incorrecta.
3. La solucion propuesta estructura el banco de preguntas en una aplicacion de Autoevaluacion CNA.
4. La aplicacion conserva baseline, snapshots, validaciones y revision del proveedor.
5. La infraestructura usa operacion local con sincronizacion Turso DB y soporte de OneDrive para evidencias y respaldos.
6. Los riesgos residuales se gestionan con roles, permisos, logs, backups y confirmaciones reforzadas.

## Preguntas criticas preparadas

| Pregunta del comite | Respuesta base |
|---------------------|----------------|
| ¿Por que no seguir usando Excel? | Excel sirve como entrada/salida, pero no como fuente de verdad trazable y auditable |
| ¿Por que Turso DB? | Permite sincronizacion online y reduce dependencia de un unico archivo local |
| ¿Que pasa si se fija mal la baseline? | La operacion requiere confirmacion reforzada, backup previo y registro del responsable |
| ¿Como se controla al proveedor? | Los instrumentos se exportan desde version aprobada y la revision se registra por instrumento/audiencia |
| ¿Donde esta la continuidad? | Base local, Turso DB remoto, snapshots y respaldos en OneDrive |

## Tareas definidas

| Tarea | Responsable | Entregable |
|-------|-------------|------------|
| Consolidar resumen ejecutivo | Todo el equipo | `taller-8/entrega/resumen-ejecutivo.md` |
| Preparar matriz de riesgos | Todo el equipo | `taller-8/presentacion/matriz-evaluacion.md` |
| Consolidar vistas finales | Todo el equipo | `taller-8/entrega/vistas-finales/` |
| Redactar reflexiones individuales | Cada integrante | `taller-8/entrega/reflexiones/` |

## Conclusion de clase

La defensa de arquitectura debe mostrar que la solucion no es solo una aplicacion nueva. Es una forma de controlar trazabilidad, versionamiento, recuperacion y relacion con el proveedor, manteniendo una complejidad razonable para el cliente.
