# Análisis y Clasificación de Enfermedad Cardiaca e Hipertensión - ENCAVI 2015-2016 🧠🩺

Proyecto realizado usando datos públicos de la Encuesta Nacional de Calidad de Vida y Salud ENCAVI 2015-16 realizada por el Departamento de Epidemiología, Ministerio de Salud de Chile con el objetivo de detectar patrones conductuales que afectan la probabilidad de desarrollo de enfermedades .

Se ha hecho una selección de variables para predecir la presencia de enfermedad cardiaca e hipertensión mediante un modelo de Random Forest, aplicando técnicas de balanceo y validación cruzada. det

El dataset a cargar es una reducción de variables de la encuesta original (ENCAVI 2015-2016) encontrada en 
[https://epi.minsal.cl/resultados-encuestas/](https://epi.minsal.cl/wp-content/uploads/2017/06/Resultados_Abril2017_ENCAVI_2015-16_Depto_Epidemiolog%C3%ADa_MINSAL.pdf)



## 🔁 Flujo del Proyecto

Este notebook sigue una estructura modular para procesar, analizar y modelar datos de salud de la encuesta ENCAVI. A continuación se detalla cada etapa del flujo de trabajo:

### 1. **Importación de Librerías**
Se cargan librerías clave para análisis de datos, visualización, modelado (scikit-learn), y balanceo de clases (SMOTE desde `imbalanced-learn`).

### 2. **Configuración Global**
Se definen parámetros generales del experimento como:
- `N_SPLITS`: número de particiones para validación cruzada.
- `N_ESTIMATORS`: número de árboles del modelo Random Forest.
- `METRICA_WEIGHTS`: pesos personalizados para métricas.
- `RANDOM_STATE`: semilla para reproducibilidad.

### 3. **Carga de Datos**
Se cargan dos archivos `.csv`:
- Dataset principal: `encavi_reducido_convertido.csv`
- Diccionario de columnas: `diccionario_columnas.csv`

Se realiza una verificación de existencia y formato correcto de columnas.

### 4. **Renombrado de Columnas**
Utilizando el diccionario cargado, se renombran todas las columnas del dataset original para facilitar su comprensión y análisis.

### 5. **Preprocesamiento**
- Se aplica **One-Hot Encoding** a variables categóricas específicas (`Sexo`, `fumador`) usando `pd.get_dummies()` con `drop_first=True`.
- Se crea un nuevo DataFrame `df_preprocesado` con las variables codificadas.
- Paralelamente, se genera una copia del DataFrame renombrado (`df_modelo`) para mantener una versión limpia para análisis o visualizaciones adicionales.

### 6. **Análisis Exploratorio**
Se analiza el DataFrame renombrado (`df_renombrado`) para obtener:
- Información general (`info()`).
- Estadísticas descriptivas (`describe()`).
- Conteo de valores nulos por columna.

### 7. **Selección de Variables y Preparación del Modelo**
- Se define la variable objetivo (`y`) y las variables predictoras (`X`) a partir del `df_preprocesado`.
- Se crea un conjunto de validación cruzada estratificada usando `StratifiedKFold`.

### 8. **Balanceo de Clases con SMOTE**
- Se aplica **SMOTE (Synthetic Minority Over-sampling Technique)** dentro del ciclo de validación cruzada para evitar el desbalance de clases.
- SMOTE se ajusta solamente al conjunto de entrenamiento en cada fold, evitando data leakage.

### 9. **Entrenamiento con Random Forest**
- Se entrena un modelo `RandomForestClassifier` en cada fold del `StratifiedKFold`.
- Se calculan métricas por fold como:
  - Accuracy
  - ROC AUC
  - Precisión, Recall, F1
  - Matriz de confusión

### 10. **Evaluación Global del Modelo**
- Se realiza un promedio de métricas sobre todos los folds.
- Se pueden visualizar:
  - **Curvas ROC** por fold
  - **Importancia de características**
  - **Matrices de confusión agregadas**

### 11. **Threshold Personalizado (si aplica)**
- En lugar de usar un umbral estándar de 0.5 para clasificación, el script puede evaluar otros thresholds basados en la métrica combinada ponderada (`METRICA_WEIGHTS`), permitiendo ajustar sensibilidad y especificidad.

### 12. **Visualización y Análisis Final**
- Se generan gráficos para interpretar resultados, como:
  - Distribución de probabilidades predichas
  - Comparaciones entre clases reales y predichas
  - Importancia de variables más relevantes

### 13. **Preparación para Producción o Reutilización**
- El código está estructurado para permitir fácil modificación e integración de otros modelos o datasets.
- Puede extenderse para análisis por subgrupos (sexo, edad, comuna, etc.).

## 🧪 Tecnologías utilizadas

- Python 3
- pandas, matplotlib, seaborn
- scikit-learn
- imbalanced-learn

## 📁 Estructura del proyecto

```
encavi2025RF/
├── encavi2025RF.ipynb           # Notebook principal
├── data/                        # Aquí se colocan los archivos CSV del proyecto
├── requirements.txt             # Librerías necesarias
├── .gitignore                   # Exclusiones típicas
└── README.md                    # Este archivo
```

## 🚀 Cómo ejecutar

1. Clona este repositorio.
2. Instala las dependencias:

```bash
pip install -r requirements.txt
```

3. Coloca los archivos CSV (`encavi_reducido_convertido.csv` y `diccionario_columnas.csv`) dentro de la carpeta `data/`.
4. Abre el notebook `encavi2025RF.ipynb` en Jupyter o VSCode.

## 📌 Notas

- El proyecto está estructurado para fácil extensibilidad hacia otros modelos (XGBoost, redes neuronales, etc.).
