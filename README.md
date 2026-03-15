# Análisis de Datos — TMDB Movies Dataset 2024

Proyecto de la **cátedra de Análisis de Datos del CEIA - Grupo 9**.

Integrantes:

- Matías Guillermo Alfaro
- Rodrigo Hernández
- Gonzalo Cuervo
- Nicolas Alberto Tonnelier
- Marina Andrea Racciatti

Análisis exploratorio de datos (EDA) sobre el dataset **TMDB Movies Dataset 2024**, que contiene información de películas (presupuesto, ingresos, popularidad, géneros, productoras, países, palabras clave, etc.).

## Setup inicial

Si vas a modificar los notebooks y hacer commits, necesitás configurar `nbstripout` para mantener limpios los notebooks en el repositorio:

```bash
# Instalar dependencias de desarrollo
uv sync --group dev

# Configurar nbstripout (una sola vez)
uv run nbstripout --install
```

Esto configura un filtro de Git que automáticamente limpia las salidas de los notebooks al hacer commit, evitando archivos innecesarios en el repositorio.

## Cómo ejecutar el notebook

### Con uv

1. Instalar [uv](https://docs.astral.sh/uv/) si no lo tenés.
2. En la raíz del proyecto:

```bash
uv init
uv sync
uv run jupyter notebook EDA_movies.ipynb
```

O para JupyterLab:

```bash
uv run jupyter lab
```

### Con Google Colab

1. Subí el notebook `EDA_movies.ipynb` a Google Drive o cloná el repo.
2. Abrí el archivo en [Google Colab](https://colab.research.google.com/).
3. El dataset se puede cargar desde Kaggle (vía `kagglehub`) o subiendo el CSV manualmente. Ajustá la celda de carga de datos según cómo tengas el archivo (por ejemplo, subiendo el CSV al entorno de Colab).

### Con un entorno Python (venv + pip)

1. Crear y activar el entorno:

```bash
python -m venv .venv
source .venv/bin/activate   # En Windows: .venv\Scripts\activate
```

2. Instalar dependencias:

```bash
pip install -e .
# o, si tenés requirements: pip install -r requirements.txt
```

3. Ejecutar Jupyter:

```bash
jupyter notebook EDA_movies.ipynb
```

## Issues

- **Muchos 0s, especialmente en `revenue` y `budget`:** IMDB usa el valor 0 como "unknown" y `revenue` y `budget` tienen > 90% de unknown values. Se agregaron variables especiales `*_valid` (ejemplo, `budget_valid`) para calcular métricas evitando el sesgo de nulls.
- **Películas que no son de 2024** Deberíamos filtrarlas?
- **Columnas en formato array:** Las columnas `genre`, `production_companies`, `production_countries` y `keywords` vienen como arrays/listas. Hay que “aplanarlas” (flatten) o expandirlas para poder analizar bien su relación con otras variables.

## TODO

- [ ] Agregar data de las variables categóricas
- [ ] Agregar gráficos de cuartiles, distancia intercuartil, etc.

## Ideas

- Explorar relaciones: budget–revenue, language–revenue, popularity–budget, genres–popularity, keywords–popularity
- Keywords por cantidad (por ejemplo, heatmap)
- Revenue y Popularity por país y por productora
- Popularity y Revenue por idioma y por género
- ¿Mayor revenue implica mayor popularity?
- Revenue negativo y su relación con otras variables
