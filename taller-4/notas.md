# 🗒️ Registro de Trabajo en Clase - Taller 4

## 📆 Fecha de la sesión
07/03/2026

## 👥 Integrantes presentes
- Carlos David Cruz Pavas (CarlosDaCruz)
- Juan Felipe Cepeda Uribe
- Esteban Fernando Forero Montejo (EstebanForero)

## 🧠 Actividades realizadas en clase

Describa brevemente qué se hizo durante la sesión:

- ¿Qué se discutió con el equipo?
  - Se analizó la infraestructura híbrida de RedExpress (nube, servidores regionales, centros de distribución y app móvil de mensajeros).
  - Se identificaron riesgos principales: latencia en rastreo en tiempo real, puntos únicos de falla y límites de escalabilidad por zonas geográficas.
- ¿Qué decisiones de modelado se tomaron?
  - Diseñar entrada por DNS/CDN/WAF y balanceador global por región.
  - Incluir API Gateway regional, módulos de procesamiento de rutas y estados de paquetes, y servicios de tracking.
  - Proponer base de datos distribuida con replicación multi-región, cache distribuido y cola de eventos para desacoplar procesos críticos.
  - Incorporar monitoreo centralizado con métricas, logs, trazas y alertas.
- ¿Qué herramientas se usaron (papel, pizarra, draw.io, Astah)?
  - Se realizó el análisis preliminar en clase con esquema conceptual para luego pasarlo a herramienta visual.
  - El diagrama se realizo con Eraser IO para modelar la arquitectura que se dejo por escrito
- ¿Qué parte del trabajo se alcanzó a desarrollar?
  - Se completó la descripción del mapa preliminar de infraestructura.
  - Se completo el mapa de la infra estructura
  - Se listaron zonas sensibles de carga, disponibilidad, monitoreo y redundancia.
  - Se documentaron problemas probables y acciones de mitigación para socializar con el docente.

## 🧩 Boceto inicial del modelo

Descripción del mapa preliminar:

1. Clientes (`App móvil` y `Web`) ingresan por `DNS + CDN + WAF`.
2. El tráfico pasa por `Balanceador global` que enruta por regiones.
3. Cada región opera con `API Gateway` y servicios críticos:
   - Tracking en tiempo real
   - Gestión de envíos
   - Procesamiento de rutas
   - Estados de paquetes
4. Los eventos de operación fluyen por `cola/bus de mensajes`.
5. Persistencia en `base de datos distribuida` (replicación multi-región) + `cache distribuido`.
6. Capa de `monitoreo y alertas` para observabilidad y respuesta a incidentes.

<img width="1229" height="944" alt="image" src="https://github.com/user-attachments/assets/b32374eb-3495-4def-bda1-c40466242824" />


Zonas críticas diagnosticadas:
- Latencia en rastreo en tiempo real por alta frecuencia de eventos.
- Riesgo de puntos únicos de falla en gateway o componentes centrales como el load balancers
- A la hora de escalar horizontalmente entre zonas es importante tener en cuenta la replicacion y sincronizacion de las bases de datos
- La dependencia de provedores en la nube como AWS, CLOUDFLARE, o GOOGLE para proveer, el CDN

## 🔁 Tareas definidas para complementar el taller

Anote las responsabilidades acordadas entre los miembros del equipo para completar la entrega final:

| Tarea asignada | Responsable | Fecha estimada |
|----------------|-------------|----------------|
| Diagrama final de infraestructura en draw.io | Carlos David Cruz Pavas | 09/03/2026 |
| Documento de diagnóstico técnico (latencia, SPOF, escalabilidad) | Carlos David Cruz Pavas | 09/03/2026 |
| Consolidación de riesgos y estrategias de mitigación | Juan Felipe Cepeda Uribe | 10/03/2026 |
| Revisión final, formato y entrega del taller | Esteban Fernando Forero Montejo | 10/03/2026 |

---

_Este documento resume el trabajo colaborativo realizado durante la sesión del taller 4 en el curso AREM - Universidad de La Sabana._
