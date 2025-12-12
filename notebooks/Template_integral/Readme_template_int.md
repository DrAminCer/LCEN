# Template integral (1→2→3): Instalación → EDA → Preprocesamiento

Este repositorio contiene el notebook **`Template_Instalacion_EDA_Prepro.ipynb`**, un flujo base para proyectos de ciencia de datos y aprendizaje automático en Python. El objetivo es ofrecer una guía reproducible que cubre:

1. **Instalación y entorno**
2. **Análisis exploratorio de datos (EDA)**
3. **Preprocesamiento y modelado básico (clasificación o regresión)**

Está pensado como punto de partida para proyectos reales y para uso docente.

---

## 1. Objetivos del template

- Estandarizar el flujo de trabajo inicial de un proyecto de datos.
- Asegurar **reproducibilidad** (semilla global, estructura de carpetas fija).
- Incluir un **EDA mínimo** siempre presente (tablas + gráficos).
- Definir un **pipeline de preprocesamiento** con `ColumnTransformer` y `Pipeline`.
- Ofrecer un **modelo base** (clasificación o regresión) con evaluación y validación cruzada.

---

## 2. Flujo general del notebook

El notebook está organizado en secciones numeradas:

### 1) Instalación y Entorno
- Revisión de opciones de entorno (local, VS Code, PyCharm, Colab).
- Verificación de versiones de Python y librerías clave:
  - `numpy`, `pandas`, `matplotlib`, `scikit-learn`, `scipy`.
- Definición de rutas de proyecto:
  - `PROJ_DIR` → directorio raíz del proyecto.
  - `DATA_DIR` → carpeta de datos (`data/`).
  - `OUTPUT_DIR` → salidas (`outputs/`).
  - `FIG_DIR` → figuras (`outputs/figs/`).
- Semilla global (`SEED`) para reproducibilidad.

### 2) EDA (Análisis Exploratorio)
- Carga de datos desde `DATA_DIR` (CSV/Excel/Parquet/SQL).
- Opción de dataset sintético de demostración si no se carga nada.
- Inspección rápida:
  - `shape`, `dtypes`, `head`, `sample`, `describe`, `info`.
- EDA visual básico:
  - Histogramas, boxplots y otros gráficos simples con `matplotlib`.
- EDA automatizado (opcional, comentado en el código):
  - `sweetviz`
  - `ydata-profiling`

### 3) Preprocesamiento y modelado
- Definición de la variable objetivo `TARGET` (por defecto: `'grupo'`).
- División en `X` (predictores) e `y` (objetivo).
- División en entrenamiento y prueba (`train_test_split`), con estratificación automática si el problema es de clasificación.
- Identificación automática de columnas numéricas y categóricas:
  - `num_cols` → columnas numéricas.
  - `cat_cols` → columnas categóricas.
- Definición de pipelines:
  - `numeric_pipe`: `SimpleImputer(strategy="median")` + `StandardScaler`.
  - `categorical_pipe`: `SimpleImputer(strategy="most_frequent")` + `OneHotEncoder(handle_unknown="ignore", sparse_output=False)`.
- Combinación en un `ColumnTransformer`:
  - `preprocess = ColumnTransformer([...])`.
- Detección de tipo de problema:
  - `is_classification = (y.nunique() <= 20)`.
- Construcción del pipeline final:
  - Clasificación: `LogisticRegression(max_iter=500)`.
  - Regresión: `LinearRegression()`.
- Entrenamiento y evaluación:
  - Clasificación: `classification_report`.
  - Regresión: `mean_squared_error`.
- Validación cruzada opcional:
  - Uso de `cross_val_score` y `StratifiedKFold` si aplica.
  - Métricas:
    - Clasificación: `accuracy`.
    - Regresión: `neg_mean_squared_error`.

### 4) Apéndices
- Sección reservada para ejemplos adicionales, variaciones de codificación y fragmentos reutilizables.

---

## 3. Requisitos

### Python

- Python 3.8 o superior.

### Paquetes principales

Mínimo:

- `numpy`
- `pandas`
- `matplotlib`
- `scikit-learn`
- `scipy`
- `jupyter` o `notebook`/`jupyterlab`

Opcionales (para EDA automatizado):

- `sweetviz`
- `ydata-profiling`

Instalación sugerida:

```bash
pip install numpy pandas matplotlib scikit-learn scipy jupyter
pip install sweetviz ydata-profiling  # opcional

Este módulo forma parte del sistema de análisis clínico del **Laboratorio Clínico de Enfermedades Neurodegenerativas (LCEN–INNN)** 

Adapta este archivo README.md para tu proyecto específico (por ejemplo, añadiendo secciones de contexto científico, referencias, o instrucciones adicionales).
