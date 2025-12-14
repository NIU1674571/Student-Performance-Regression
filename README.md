# Student-Performance-Regression

## 🧠 Objetivo: Predicción de la nota media de los estudiantes

## 📌 Descripción general

Este proyecto tiene como objetivo desarrollar y evaluar modelos de **regresión** que permitan predecir la **nota media (`average_score`)** de un estudiante (conjunto de estudiantes) a partir de sus características personales y académicas.

La nota media se ha construido como la media de tres puntuaciones originales del dataset:

- `math score`
- `reading score`
- `writing score`

A partir de esta nueva variable objetivo (`average_score`), se entrena un modelo capaz de estimar el rendimiento académico global del alumno.

---

## 📊 Dataset

El Dataset contiene **1.000 estudiantes**, con la siguiente información:

- `gender`  
- `race/ethnicity`  
- `parental level of education`  
- `lunch`  
- `test preparation course`  
- `math score`
- `reading score`
- `writing score`

A partir de estas tres últimas se crea el atributo (`average_score`) que sera el objetivo a predecir:
- `average_score`

---

## 🔍 Enfoque del proyecto

### Preprocesamiento
- Creación de `average_score` como media de `math score`, `reading score` y `writing score`.
- Comprobación de valores nulos.
- Codificación de variables categóricas:
  - `LabelEncoder`: `gender`, `lunch`, `test preparation course`.
  - `OneHotEncoder`: `race/ethnicity`, `parental level of education`.
- División en **train y test **.

### Modelado y validación
- Modelos probados:
  - `LinearRegression`, `KNeighborsRegressor`, `DecisionTreeRegressor`,
    `RandomForestRegressor`, `GradientBoostingRegressor`.
- Validación cruzada con **KFold (k=10)**.
- Métricas usadas para evaluación: **MAE**, **RMSE** y **R²**.
