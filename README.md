# Pyxoom · Visualizador de Competencias — Sumimsa

Herramienta interactiva para visualizar y analizar resultados de evaluaciones de competencias Pyxoom.

Desarrollada por **London Consulting Group** para **Sumimsa**.

## Características

- **Carga de datos**: Drag & drop o file picker para archivos Excel (.xlsx, .xls, .csv)
- **Auto-detección**: Identifica automáticamente columnas de nombre, nivel, departamento y competencias
- **4 vistas de análisis**:
  - Vista General — KPIs, radar Real vs Ideal, distribución, brechas
  - Por Nivel Jerárquico — comparativo entre niveles con benchmarks ajustados
  - Por Departamento — comparativo entre áreas, tabla resumen
  - Por Persona — perfil individual, radar vs ideal y vs promedio empresa
- **Benchmarks ideales**: Basados en mejores prácticas, ajustados por nivel jerárquico
- **Self-contained**: Un solo archivo HTML, sin backend, listo para GitHub Pages

## Uso rápido

```bash
# Clonar y abrir
git clone <repo-url>
cd pyxoom-sumimsa
open index.html
```

O servir localmente:

```bash
npx serve .
```

## Formato del Excel esperado

| Nombre | Nivel | Departamento | Liderazgo | Comunicación | ... |
|--------|-------|--------------|-----------|--------------|-----|
| Juan Pérez | Nivel 1 - Dirección | Ventas | 4.2 | 3.8 | ... |

- Las columnas de competencias deben contener valores numéricos del 1 al 5
- Los nombres de columnas se detectan automáticamente por patrones comunes

## Tecnologías

- HTML/CSS/JS vanilla
- [Chart.js](https://www.chartjs.org/) — gráficos interactivos
- [SheetJS](https://sheetjs.com/) — parseo de Excel en el navegador

## Licencia

Uso interno — London Consulting Group © 2026
