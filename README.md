# Talleres en Clase — Arquitectura Empresarial

**Curso:** Arquitectura Empresarial — Universidad de La Sabana  
**Semestre:** 2026-1

## Equipo

| Nombre | GitHub |
|--------|--------|
| Carlos David Cruz Pavas | `CarlosDaCruz` |
| Juan Felipe Cepeda Uribe | — |
| Esteban Fernando Forero Montejo | `EstebanForero` |

---

## Estructura

```
talleres-en-clase/
├── taller-1/                   ← BPMN: caso base Clínica Salud Viva
│   ├── clase/
│   │   ├── notas.md
│   │   ├── diagram.bpmn
│   │   └── diagram.png
├── taller-2/                   ← ERD: caso base Clínica Salud Viva
│   ├── clase/
│   │   ├── notas.md
│   │   ├── ERD.jpg
│   │   ├── Sketch.jpg
│   │   └── erd-export-*.png
├── taller-4/                   ← Infraestructura: caso base RedExpress
│   ├── caso-clase.md
│   ├── notas.md
│   └── diagrama-infra.png
├── taller-5/                   ← Seguridad STRIDE: caso base EdukIT
│   ├── caso-clase.md
│   ├── notas.md
│   ├── plantilla_analisis_stride_seguridad.xlsx
│   └── stride_analisis.xlsx
├── taller-6/                   ← Cumplimiento normativo: caso base GobData
│   ├── caso-clase.md
│   ├── notas.md
│   └── clase/
│       └── checklist-gobdata.xlsx
├── taller-7/                   ← Integración de vistas: trabajo en clase
│   └── notas.md
├── taller-8/                   ← Comité de Arquitectura: trabajo en clase
│   └── notas.md
└── taller-9/                   ← Análisis de riesgos: trabajo en clase
    └── notas.md
```

---

## Relación con talleres-empresa

Cada taller tiene dos componentes:
- **En clase** (este repo): caso base genérico trabajado durante la sesión.
- **Entrega** (`talleres-empresa/`): aplicación al cliente real — Dirección de Desarrollo Estratégico, Universidad de La Sabana.

| Taller | Caso base (clase) | Cliente real (empresa) |
|--------|-------------------|------------------------|
| 1 | Clínica Salud Viva — agendamiento de citas (BPMN) | DDE — banco de preguntas CNA (BPMN) |
| 2 | Clínica Salud Viva — dominio de información (ERD) | DDE — estructura CNA, preguntas, audiencias (ERD) |
| 4 | RedExpress — infraestructura logística | DDE — infraestructura AS-IS y TO-BE |
| 5 | EdukIT — análisis STRIDE de pagos | DDE — STRIDE sobre flujo de actualización CNA |
| 6 | GobData — cumplimiento normativo | DDE — Ley 1581, Decreto 1377, ISO 27001 |
| 7 | Integración de vistas | DDE — tablero integrado de vistas |
| 8 | Comité de Arquitectura | DDE — consolidación final con C4 y gobierno operativo |
| 9 | Análisis de riesgos | DDE — riesgos AS-IS vs TO-BE |
