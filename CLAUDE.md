# Pyxoom Sumimsa — Visualizador de Competencias

## Qué es este proyecto

Herramienta HTML interactiva single-file para visualizar resultados de evaluaciones de competencias Pyxoom del cliente **Sumimsa** de London Consulting Group (LCG).

El archivo principal es `index.html` — un HTML self-contained (~900 líneas) que carga datos desde archivos Excel y genera dashboards interactivos con gráficos.

## Stack técnico

- **HTML/CSS/JS** puro (sin framework, sin build step)
- **Chart.js 4.4.1** (CDN) — gráficos radar, barras, distribución
- **SheetJS/xlsx 0.18.5** (CDN) — parseo de archivos Excel en el navegador
- **Sin dependencias locales** — todo vía CDN, self-contained

## Estructura del archivo

```
index.html
├── <style>        → CSS completo (variables, responsive, componentes)
├── <body>         → Markup de las 5 vistas (tabs)
└── <script>       → Lógica completa
    ├── STATE      → Variables globales (DATA, COMPETENCIAS, NIVELES, DEPTOS)
    ├── IDEAL_BASE → Benchmarks ideales por competencia y nivel jerárquico
    ├── File handling → Drag & drop, file picker, parseWorkbook()
    ├── detectColumns() → Auto-detección de columnas del Excel
    ├── loadDemoData()  → Datos de demostración (40 personas, 10 competencias)
    ├── renderGeneral() → Vista general empresa
    ├── renderNivel()   → Vista por nivel jerárquico
    ├── renderDepto()   → Vista por departamento
    └── renderPersona() → Vista individual con detalle
```

## Modelo de datos

Cada persona en DATA tiene esta forma:
```js
{
  nombre: "Carlos Mendoza",
  nivel: "Nivel 1 - Dirección",
  depto: "Ventas",
  scores: {
    "Liderazgo": 4.2,
    "Comunicación": 3.8,
    // ... una entrada por competencia, valor 1-5
  }
}
```

## Benchmarks ideales (IDEAL_BASE)

Los ideales están definidos en el objeto `IDEAL_BASE` y varían por nivel jerárquico:
- **Nivel 1 (Dirección)** y **Nivel 2 (Gerencia)**: Ideales altos (4.5-5) en Liderazgo, Pensamiento Estratégico, Toma de Decisiones
- **Nivel 3-5**: Ideales progresivamente menores en competencias de dirección, pero altos en Trabajo en Equipo, Enfoque al Cliente

Si el cliente tiene benchmarks propios, modificar `IDEAL_BASE` y `DEFAULT_IDEAL`.

## Parser de Excel (detectColumns)

El parser auto-detecta columnas buscando patrones:
- **Nombre**: columnas con "nombre", "empleado", "colaborador", "participante", "evaluado"
- **Nivel**: "nivel", "puesto", "posición", "jerarquía", "cargo"
- **Departamento**: "departamento", "depto", "área", "dirección", "gerencia"
- **Competencias**: cualquier columna con >50% de valores numéricos entre 0-5

Si la sábana real tiene nombres de columna diferentes, ajustar los arrays `namePatterns`, `nivelPatterns`, `deptoPatterns` en `detectColumns()`.

## Cómo correr localmente

```bash
# Opción 1: Python
python3 -m http.server 8080

# Opción 2: Node
npx serve .

# Opción 3: Abrir directamente
open index.html
```

## Deploy en GitHub Pages

1. Push a un repo de GitHub
2. Settings → Pages → Source: main branch, root (/)
3. El archivo `index.html` se sirve automáticamente

## Tareas pendientes / mejoras posibles

- [ ] Cargar el Excel real de Sumimsa y validar que el parser detecte bien las columnas
- [ ] Ajustar benchmarks ideales a las competencias específicas de Pyxoom/Sumimsa
- [ ] Agregar logo real de Sumimsa (actualmente es texto placeholder)
- [ ] Para niveles altos, destacar "Pensamiento Estratégico" como competencia clave
- [ ] Agregar exportación a PDF de cada vista
- [ ] Agregar modo comparativo (seleccionar 2+ personas side-by-side)
- [ ] Agregar heatmap de competencias por departamento
- [ ] Considerar dark mode
