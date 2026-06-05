# Sesgos de Género en el Diagnóstico Psiquiátrico · 1990–2021

**Visualización scrollytelling interactiva** sobre sesgos de género en el diagnóstico de trastornos mentales, basada en el Global Burden of Disease Study 2021.

🔗 **[Ver visualización en vivo](https://pilar-orozco.github.io/gender-bias-mental-health/)**

## Descripción

Esta visualización narrativa explora cómo el sistema psiquiátrico diagnostica de forma sistemáticamente diferente según el sexo del paciente, usando datos epidemiológicos del GBD 2021 (IHME, University of Washington).

### Estructura narrativa

| Capítulo | Contenido |
|----------|-----------|
| 1 · El punto de partida | Contexto sobre sesgos diagnósticos de género |
| 2 · El nudo | Prevalencia estimada vs. diagnóstico clínico por trastorno |
| 3 · Caso TLP | El Trastorno Límite de Personalidad: 75% mujeres |
| 4 · Las invisibles | TDAH: infradiagnóstico femenino por grupo de edad |
| 5 · Tendencias 1990–2021 | Evolución temporal interactiva con slider |
| 6 · Geografía | Correlación GII × brecha diagnóstica (scatter) |

### Preguntas de investigación respondidas

- **P1**: ¿Qué trastornos presentan mayor brecha y cómo ha evolucionado 1990–2021?
- **P2**: ¿El TLP, TDAH y T. alimentarios muestran sesgos coherentes con la literatura?
- **P3**: ¿Los países con mayor igualdad de género (GII) tienen menor brecha diagnóstica?
- **P4**: ¿Cómo varía la carga de enfermedad (DALYs) por sexo y grupo de edad?
- **P5**: ¿Hay convergencia temporal en trastornos históricamente sesgados?

## Tecnologías

- **ScrollMagic 2.0.8** — animaciones basadas en scroll
- **GSAP 3.12 + ScrollTrigger** — animaciones fluidas
- **D3.js v7** — gráficos interactivos (barras divergentes, líneas, scatter, donuts)
- HTML5 / CSS3 — diseño responsivo, sin frameworks

## Datos

| Fuente | Descripción |
|--------|-------------|
| [GBD 2021 · IHME](https://vizhub.healthdata.org/gbd-results/) | Prevalencia, incidencia y DALYs por trastorno mental, sexo, edad y país · 1990–2021 |
| [GII · PNUD](https://hdr.undp.org/data-center/thematic-composite-indices/gender-inequality-index) | Índice de Desigualdad de Género por país · 2023 |
| Literatura clínica | Ratios diagnósticas de referencia (Björkenstam et al., JAMA 2021; OMS 2023) |

> Los valores de prevalencia son estimaciones del GBD 2021. Las ratios diagnósticas son valores de referencia de la literatura revisada.

## Autoría

**Pilar Orozco del Moral** · p.orozcod@uoc.edu  
M2.859 Visualización de Datos · Universitat Oberta de Catalunya · 2025

## Licencia

[MIT License](LICENSE) — libre uso, modificación y distribución con atribución.
