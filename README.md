# Student-Performance-Regression

🧠 **Objetivo: Predicción de la nota media de los estudiantes**

## 📌 Descripción general

Este proyecto tiene como objetivo desarrollar y evaluar modelos de **regresión** que permitan predecir la **nota media (`average_score`)** de un estudiante a partir de sus características personales y académicas.

La nota media se ha construido como la media de tres puntuaciones originales del dataset:

- `math score`
- `reading score`
- `writing score`

A partir de esta nueva variable objetivo (`average_score`), se entrena un modelo capaz de estimar el rendimiento académico global del alumno.

---

## 📊 Dataset

El conjunto de datos contiene **1.000 estudiantes**, con la siguiente información principal:

- `gender`  
- `race/ethnicity`  
- `parental level of education`  
- `lunch`  
- `test preparation course`  
- `math score`, `reading score`, `writing score`

A partir de estas tres últimas se crea el atributo:

- `average_score` → objetivo a predecir.

No se han encontrado valores nulos en ninguna columna, por lo que no ha sido necesario aplicar técnicas de imputación.

---

## 🔍 Enfoque del proyecto

### 1. Análisis exploratorio

- Análisis descriptivo de las notas (`math`, `reading`, `writing`) y de `average_score`.
- Estudio de la distribución de las variables categóricas:
  - `gender`
  - `race/ethnicity`
  - `parental level of education`
  - `lunch`
  - `test preparation course`
- Análisis de cómo cambia `average_score` según cada variable categórica (boxplots por grupo).
- Matriz de correlación entre todas las variables ya codificadas, incluyendo `average_score`, para comprobar:
  - qué atributos se relacionan más con la nota,
  - y si hay correlaciones fuertes entre predictores (redundancias).

### 2. Preprocesamiento

- **Creación de la variable objetivo**:  
  `average_score = media(math score, reading score, writing score)`.

- **Tratamiento de valores nulos**:
  - Visualización con `missingno` y recuento con `isnull().sum()`.
  - Se confirma que no hay valores faltantes.

- **Codificación de variables categóricas**:

  - `LabelEncoder` para variables binarias:
    - `gender` (0/1)  
    - `lunch` (0/1)  
    - `test preparation course` (0/1)

  - `OneHotEncoder` para variables con más de dos categorías:
    - `race/ethnicity` (grupos A, B, C, D, E)  
    - `parental level of education` (high school, some college, bachelor’s, master’s, etc.)

  De esta forma, todas las variables quedan en formato numérico y listas para ser usadas por los modelos.

- **División entrenamiento / test**:
  - `train_test_split` con un **80 % para entrenamiento** y **20 % para test**.

- **Normalización**:
  - No ha sido necesaria la normalización de variables numéricas adicionales, ya que el modelo seleccionado final es una regresión lineal sobre variables ya escaladas de forma razonable y sin valores extremos.

---

## 🤖 Modelado y validación

Se han entrenado varios modelos de regresión usando **validación cruzada con KFold (k=10)** y las métricas:

- **MAE** (Error Absoluto Medio)  
- **RMSE** (Raíz del Error Cuadrático Medio)  
- **R²** (coeficiente de determinación)

Modelos probados:

- `LinearRegression`
- `KNeighborsRegressor`
- `DecisionTreeRegressor`
- `RandomForestRegressor`
- `GradientBoostingRegressor`

Para cada modelo se calculan los valores medios de MAE, RMSE y R² en los 10 folds.  
Además, se dibujan **curvas de aprendizaje** (MAE de entrenamiento y de validación) para analizar:

- si el modelo sobreajusta o no,
- y cómo mejora el error al aumentar el tamaño del conjunto de entrenamiento.

---

## 📈 Resultados principales

- El modelo que obtiene el **mejor equilibrio** entre error y capacidad de explicación es **LinearRegression**.
- En validación cruzada:
  - MAE medio ≈ 10 puntos.
  - RMSE medio ≈ 12–13 puntos.
  - R² medio positivo, mejor que el resto de modelos probados.
- En el conjunto de **test**:
  - **MAE ≈ 9.8**  
  - **RMSE ≈ 12.4**  
  - **R² ≈ 0.27**

Esto significa que el modelo se equivoca de media unos **10 puntos** sobre una escala de 0 a 100, y es capaz de explicar aproximadamente un **27 %** de la variabilidad de las notas.

También se incluye un **gráfico de dispersión** de:

- `average_score` real (eje X)  
- `average_score` predicho (eje Y)

con una línea roja `y = x` como referencia. Los puntos se concentran alrededor de esa línea, sobre todo entre notas medias (50–80), lo que indica que el modelo sigue bien la tendencia, aunque tiene más dificultad con notas muy bajas o muy altas.

---

## ✅ Conclusiones

- El modelo de **regresión lineal** ofrece un rendimiento **razonable** y consistente entre validación cruzada y test.
- El error medio (MAE) es moderado y el R² muestra que el modelo captura parte, pero no toda, de la información relevante sobre el rendimiento académico.
- El modelo funciona especialmente bien para estudiantes con notas medias, y le cuesta más predecir notas extremas (muy bajas o muy altas).

---

## 🚀 Trabajo futuro

Algunas posibles mejoras:

- Incluir **nuevas variables** relacionadas con:
  - hábitos de estudio,
  - horas de dedicación,
  - asistencia a clase,
  - contexto socioeconómico, etc.
- Probar **modelos más complejos** (p. ej. Random Forest, Gradient Boosting con mejor ajuste) junto con una búsqueda sistemática de **hiperparámetros** (`GridSearchCV` o `RandomizedSearchCV`).
- Explorar técnicas de **ingeniería de características** adicionales:
  - combinaciones de variables,
  - variables agregadas,
  - detección y tratamiento más fino de outliers.

---

## 🗂 Estructura del repositorio

- `dataset/` → fichero(s) CSV con los datos de estudiantes.  
- `students.ipynb` → notebook principal con:
  - análisis exploratorio,
  - preprocesamiento,
  - selección de modelos,
  - validación cruzada,
  - evaluación en test y conclusiones.
- `README.md` → este documento.

---

## 💻 Tecnologías utilizadas

- **Python 3**
- **pandas, numpy**
- **seaborn, matplotlib, missingno**
- **scikit-learn** (`LabelEncoder`, `OneHotEncoder`, `LinearRegression`, `KNeighborsRegressor`, `DecisionTreeRegressor`, `RandomForestRegressor`, `GradientBoostingRegressor`, `KFold`, `cross_validate`, `learning_curve`, `mean_absolute_error`, `mean_squared_error`, `r2_score`)

