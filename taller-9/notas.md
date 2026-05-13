# Analisis de Riesgos - Taller 9

## Integrantes

- Carlos David Cruz Pavas (CarlosDaCruz)
- Juan Felipe Cepeda Uribe
- Esteban Fernando Forero Montejo (EstebanForero)

## Contexto del sistema

El sistema evaluado es la aplicacion de Autoevaluacion CNA que se esta desarrollando. La aplicacion busca reemplazar un flujo anterior basado principalmente en archivos Excel consolidados, manejo manual de preguntas, control informal de versiones y revision externa con baja trazabilidad.

La solucion nueva centraliza la informacion en una base de datos local compatible con libSQL/Turso, importa los consolidados de Excel, normaliza la jerarquia CNA, administra el banco de preguntas, conserva una linea base original, valida condiciones antes de exportar, genera instrumentos con comparacion de cambios y permite revisar entregas del proveedor por instrumento/audiencia.

## Riesgos de la aplicacion anterior

En la aplicacion o proceso anterior, el mayor problema no era solo tecnico. El riesgo principal era que la informacion dependia demasiado de archivos editados manualmente, criterios operativos poco controlados y conocimiento de personas especificas. Esto generaba errores dificiles de detectar, duplicados, perdida de trazabilidad y poca confianza al momento de entregar instrumentos o revisar cambios.

| Riesgo | Causa | Impacto | Probabilidad | Arquitectura afectada | Mitigacion propuesta |
|--------|-------|---------|--------------|------------------------|----------------------|
| Dependencia de Excel manuales | Los consolidados se editan directamente en archivos y no desde una fuente unica de verdad | Alto | Alta | Datos / Procesos | Centralizar el banco de preguntas en base de datos y generar exportaciones desde el sistema |
| Duplicidad de preguntas | No hay una regla tecnica fuerte que impida repetir codigos o preguntas similares | Alto | Alta | Datos | Usar unicidad por codigo de pregunta y validaciones antes de importar o exportar |
| Duplicidad de lineamientos | La jerarquia CNA puede repetirse por errores de copia, celdas combinadas o diligenciamiento incompleto | Alto | Alta | Datos / Modelo CNA | Normalizar Factor, Caracteristica y Aspecto; deduplicar por alcance y codigos CNA |
| Perdida de trazabilidad de cambios | Los archivos se modifican y circulan sin una linea base inmutable | Alto | Alta | Procesos / Gobierno TI | Definir una linea base original y comparar los cambios contra esa version |
| Versiones inconsistentes de instrumentos | Diferentes personas pueden trabajar sobre copias distintas del consolidado | Alto | Media | Procesos / Exportacion | Generar instrumentos desde la base de datos y no desde archivos editados manualmente |
| Errores por jerarquia CNA incompleta | Las celdas de Factor, Caracteristica o Aspecto pueden venir vacias por formato de Excel | Medio | Alta | Importacion / Datos | Aplicar forward-fill controlado durante la importacion |
| Falta de validacion antes de entrega | El proceso anterior puede permitir entregar instrumentos incompletos o inconsistentes | Alto | Media | Validacion / Proveedor | Crear reglas bloqueantes antes de exportar o entregar al proveedor |
| Baja auditoria de revision del proveedor | Las correcciones del proveedor se revisan sin estado formal por pregunta | Medio | Media | Provider Review / Gobierno | Registrar revision por instrumento, estado, observacion y evidencia |
| Perdida de evidencia de revision | Las evidencias pueden quedar en correos, carpetas sueltas o rutas no estandarizadas | Medio | Media | Procesos / Documentacion | Adjuntar rutas o imagenes locales en la revision y exportar reporte DOCX |
| Dependencia de personas clave | El criterio de que archivo es el correcto o que cambios se hicieron vive en la memoria del equipo | Alto | Media | Gobierno TI | Documentar reglas, snapshots, baseline y flujo de confirmacion reforzada |
| Falta de recuperacion ante errores | Si se daña un archivo o se elimina informacion, no hay snapshots consistentes del estado editable | Alto | Media | Persistencia / Continuidad | Crear historial automatico y snapshots manuales persistentes |
| Riesgo de datos no cifrados o mal protegidos | Los Excel pueden circular por carpetas compartidas sin controles suficientes | Alto | Media | Seguridad / Datos | Limitar la operacion a repositorio local controlado y definir respaldos seguros |

## Riesgos de la solucion nueva en desarrollo

La solucion nueva reduce varios riesgos del proceso anterior porque introduce base de datos, reglas de unicidad, linea base original, validaciones y exportaciones controladas. Aun asi, tambien aparecen nuevos riesgos propios de una aplicacion local con persistencia, importacion de archivos, generacion de documentos y sincronizacion con OneDrive/Microsoft Graph.

| Riesgo | Causa | Impacto | Probabilidad | Arquitectura afectada | Mitigacion propuesta |
|--------|-------|---------|--------------|------------------------|----------------------|
| Base de datos local como punto unico de falla | La informacion editable queda concentrada en una base local libSQL | Critico | Media | Persistencia / Disponibilidad | Implementar respaldos frecuentes, snapshots manuales y sincronizacion controlada con carpeta de respaldo |
| Corrupcion o perdida de la base de datos | Fallos del equipo, cierre inesperado o sincronizacion incorrecta | Critico | Media | Persistencia | Mantener backups antes de fijar baseline y antes de restaurar snapshots |
| Baseline fijada por error | Un usuario podria marcar como original un contenido incorrecto | Alto | Baja | Original Baseline / Gobierno | Mantener confirmacion reforzada con texto `FIJAR ORIGINAL`, acknowledgement de reemplazo, backup y perfil guardado |
| Importacion incorrecta de Excel | Estructuras de archivo no esperadas, celdas vacias o formatos cambiantes | Alto | Media | Import / Datos | Validar columnas requeridas, forward-fill controlado, pruebas con workbook de muestra y reporte de inconsistencias |
| Deduplicacion agresiva | La normalizacion podria unir lineamientos que parecen iguales pero representan casos distintos | Medio | Media | CNA Model / Import | Revisar claves de unicidad por scope, factor, caracteristica y aspecto; dejar trazabilidad de registros omitidos |
| Codigos de aspecto generados incorrectamente | Aspectos manuales dependen de claves deterministicas generadas | Medio | Media | CNA Model | Usar generacion estable basada en factor, caracteristica y descripcion; permitir revision visual del resultado |
| Exportaciones con colores incorrectos | La comparacion por codigo y hash podria clasificar mal cambios si el baseline esta mal fijado | Alto | Media | Export / Original Baseline | Bloquear exportacion sin baseline y mostrar resumen de diferencias antes de generar archivos |
| Restauracion de snapshot equivocada | Restaurar reemplaza preguntas y lineamientos actuales | Alto | Baja | History / Persistencia | Usar confirmacion reforzada, mostrar fecha, autor y alcance del snapshot antes de restaurar |
| Historial incompleto como backup total | El snapshot no guarda todas las tablas auxiliares de la base | Medio | Media | History / Persistencia | Comunicar que snapshots cubren estado editable; mantener backup completo de base para recuperacion total |
| Falta de monitoreo operativo | Al ser aplicacion local, puede no haber observabilidad centralizada | Medio | Media | Disponibilidad / Soporte | Registrar errores de importacion, exportacion y repositorio; agregar logs locales consultables |
| Accesos locales no controlados | Si varias personas usan el mismo equipo o carpeta, pueden modificar informacion sin control | Alto | Media | Seguridad / Workspace | Guardar perfil de editor, controlar ubicacion de base, restringir permisos de carpeta y evitar usuarios compartidos |
| Exposicion por sincronizacion cloud | OneDrive o Microsoft Graph pueden sincronizar archivos sensibles o versiones intermedias | Alto | Media | Workspace / Seguridad | Definir carpeta de sincronizacion, evitar subir temporales sensibles y documentar permisos de Microsoft Graph |
| Evidencias no soportadas en DOCX | Algunos archivos adjuntos no se incrustan y solo quedan como ruta | Bajo | Media | Provider Review / Export | Mantener lista de formatos soportados y conservar rutas para formatos no embebibles |
| Dependencia de convenciones importadas | Codigos de audiencia, formatos o convenciones pueden variar entre consolidados | Medio | Media | Question Bank / Export | Generar hoja de Convencion y normalizar codigos durante importacion |
| Complejidad de modulos de persistencia | La separacion en schema, parsing, helpers, snapshots y reviews puede dificultar mantenimiento | Medio | Media | Persistencia / Gobierno TI | Mantener responsabilidades documentadas y pruebas por modulo de repositorio |

## Comparacion AS-IS vs TO-BE

| Dimension | Aplicacion anterior / AS-IS | Solucion nueva / TO-BE |
|-----------|-----------------------------|-------------------------|
| Fuente de verdad | Archivos Excel editados manualmente | Base de datos local con banco de preguntas editable |
| Control de cambios | Revision manual entre versiones | Baseline original con hashes y colores de diferencia |
| Duplicados | Alta probabilidad por copia y consolidacion manual | Indices unicos para preguntas y lineamientos |
| Trazabilidad | Baja, depende de nombres de archivo y memoria del equipo | Snapshots, baseline, estados de revision y reportes |
| Validacion | Manual y tardia | Reglas bloqueantes antes de exportar o entregar |
| Revision del proveedor | Informal o dispersa | Checklist por instrumento/audiencia con evidencia |
| Disponibilidad | Depende del archivo correcto y de quien lo tenga | Depende de la base local, respaldos y sincronizacion |
| Seguridad | Riesgo por archivos circulando en carpetas o correos | Riesgo controlable con permisos locales, perfil y carpeta definida |
| Gobierno TI | Decisiones poco documentadas | Reglas explicitas para baseline, importacion, exportacion e historial |

## Riesgos priorizados

| Prioridad | Riesgo | Razon |
|-----------|--------|-------|
| 1 | Perdida o corrupcion de la base de datos local | Afectaria todo el banco de preguntas, baseline, lineamientos y revisiones |
| 2 | Baseline fijada incorrectamente | Todas las exportaciones con colores dependerian de una referencia equivocada |
| 3 | Importacion incorrecta del consolidado | Puede crear preguntas o lineamientos mal normalizados desde el inicio del ciclo |
| 4 | Acceso local o sincronizacion cloud sin control | Puede exponer informacion academica, evidencias o instrumentos de evaluacion |
| 5 | Restauracion equivocada de snapshot | Puede reemplazar el estado actual y generar perdida operativa |

## Recomendaciones

- Mantener respaldos completos de la base antes de fijar o reemplazar la linea base original.
- Documentar claramente donde vive la base local, que carpeta se sincroniza y quien tiene acceso.
- Conservar la confirmacion reforzada para operaciones destructivas o de alto impacto.
- Agregar logs locales para importacion, exportacion, restauracion de snapshots y errores de repositorio.
- Probar cada importacion con validaciones de duplicados, jerarquia CNA y conteo de preguntas antes de permitir exportar.
- Revisar periodicamente los permisos de OneDrive y Microsoft Graph para evitar exposicion accidental.
- Mantener pruebas automaticas de importacion, deduplicacion, comparacion contra baseline y exportacion de instrumentos.

## Conclusion

El proceso anterior concentra riesgos en el trabajo manual con Excel, la falta de trazabilidad y la dependencia de personas. La solucion nueva corrige buena parte de esos problemas al mover la operacion hacia una base de datos, baseline inmutable, validaciones y exportaciones generadas desde el sistema.

Sin embargo, la nueva arquitectura tambien necesita controles propios: respaldos, gobierno de baseline, permisos locales, cuidado con sincronizacion cloud y pruebas de importacion/exportacion. El riesgo principal cambia de "no saber cual archivo es el correcto" a "proteger bien la base y las reglas que gobiernan el ciclo de autoevaluacion".
