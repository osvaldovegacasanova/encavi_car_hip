# Análisis y Clasificación de Enfermedades Crónicas - ENCAVI 2025 🧠🩺

Este proyecto utiliza datos de la Encuesta Nacional de Calidad de Vida y Salud (ENCAVI) 2025 para predecir la presencia de enfermedades crónicas mediante un modelo de Random Forest, aplicando técnicas de balanceo y validación cruzada.

## 🔍 Objetivos

- Explorar y preparar datos provenientes de ENCAVI.
- Preprocesar y codificar variables categóricas.
- Aplicar balanceo con SMOTE para enfrentar desbalance de clases.
- Entrenar y evaluar un modelo de clasificación Random Forest.
- Optimizar el flujo de trabajo para futuras predicciones en salud pública.

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
- Se puede adaptar para análisis por comuna, grupo etario o factor de riesgo específico.
