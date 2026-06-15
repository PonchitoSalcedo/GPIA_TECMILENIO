🫀 **Predicción de Ataques Cardíacos: Análisis y Modelado Predictivo**
Descripción del Proyecto:
Este proyecto se centra en la predicción de infartos utilizando un conjunto de datos con características clínicas y relacionadas con la salud. El flujo de trabajo incluye análisis exploratorio de datos (EDA), ingeniería de características, manejo de valores faltantes y atípicos, y la creación de múltiples modelos de aprendizaje automático para predecir la probabilidad de padecer una enfermedad cardíaca. El objetivo es proporcionar una herramienta de apoyo para la identificación temprana de pacientes con alto riesgo cardiovascular.


📑 **Tabla de Contenidos**
1.- Sobre el Proyecto
2.- Conjunto de Datos
3.- Análisis Exploratorio de Datos (EDA)
4.- Visualizaciones
5.- Preprocesamiento e Ingeniería de Características
6.- Modelado de Aprendizaje Automático
7.- Métricas y Evaluación de Modelos
8.- Resultados y Comparativa
9.- Conclusiones
10.- Recomendaciones para Trabajos Futuros
11.- Cómo Ejecutar el Proyecto

**1. Sobre el Proyecto**
Este proyecto fue desarrollado como parte de un análisis integral para la predicción de ataques cardíacos utilizando técnicas de machine learning. El flujo de trabajo incluye:
- Análisis Exploratorio de Datos (EDA): Inspección de estadísticas básicas, valores faltantes, valores atípicos y correlaciones.
- Visualización: Distribuciones de características clave, proporción de clases y relaciones entre variables.
- Ingeniería de Características: Manejo de outliers, creación de nuevas features, codificación y escalado.
- Modelado: Implementación de tres modelos (Regresión Logística, Random Forest y XGBoost).
- Evaluación: Cálculo de accuracy, precisión, recall, F1-score, latencia y validación cruzada.


**2. Conjunto de Datos**
<img width="1072" height="515" alt="image" src="https://github.com/user-attachments/assets/6faa7451-efd4-4515-b190-e6b543d2f982" />
<img width="1055" height="452" alt="image" src="https://github.com/user-attachments/assets/df792cf1-44d2-490c-b222-cc5b459ce671" />
Nota: Los nombres y números de seguridad social de los pacientes fueron eliminados de la base de datos y reemplazados por valores ficticios.


**3. Análisis Exploratorio de Datos (EDA)**
<img width="1112" height="406" alt="image" src="https://github.com/user-attachments/assets/24ae4f91-6795-40bf-8136-c0ae9ea99446" />

**Hallazgos clave:**
- Sin valores nulos: El dataset está completo (303 registros, 14 columnas).
- Duplicados: Se encontró 1 registro duplicado que fue eliminado.
- Distribución de target: Balanceada (54% clase 1, 46% clase 0).
- Correlaciones destacadas: Correlación positiva con cp y thalachh (mayor riesgo). Correlación negativa con exng, oldpeak, caa, thall (menor riesgo).


**4. Visualizaciones**
A continuación se resumen los hallazgos visuales obtenidos en el cuaderno de Colab. Las imágenes generadas (eda_heart_analysis.png, confusion_matrices.png, model_comparison.png, feature_importance.png) están disponibles en el repositorio o en la ejecución del código.

- Distribución de Edad por Riesgo: Los pacientes con mayor riesgo se concentran entre los 50 y 60 años, mientras que los de menor riesgo muestran una distribución   más uniforme.
- Sexo vs Riesgo: La mayoría de los pacientes son hombres (68%), y dentro de este grupo, la proporción de alto riesgo es significativamente mayor.
- Dolor de Pecho vs Target: Los pacientes con dolor asintomático (cp=4) presentan la mayor incidencia de ataques. La angina típica (cp=1) se asocia con menor        riesgo.
- Matriz de Correlación: Las variables cp, thalachh y oldpeak muestran la correlación más fuerte con la variable objetivo.
- Comparativa de Modelos: XGBoost supera consistentemente a los demás en todas las métricas evaluadas.


**5. Preprocesamiento e Ingeniería de Características**
**Manejo de outliers (método IQR - Rango Intercuartil):**
  - chol: 8 outliers tratados
  - trestbps: 5 outliers tratados
  - oldpeak: 3 outliers tratados
  - thalachh: 2 outliers tratados
  - age: 0 outliers tratados

**Extracción de nuevas características:**
  - age_group: Categorización por edad (Young, Adult, Middle, Senior)
  - chol_risk: Nivel de riesgo de colesterol (Normal, Borderline, High)
  - bp_risk: Nivel de riesgo de presión arterial (Normal, Elevated, High1, High2)
  - chol_age_ratio: Ratio colesterol/edad
  - hr_age_product: Producto frecuencia cardíaca por edad

**Transformaciones aplicadas:**
  - One-Hot Encoding aplicado a variables categóricas (sex, cp, fbs, restecg, exng, slp, caa, thall, age_group, chol_risk, bp_risk)
  - Estandarización (StandardScaler) aplicado a variables numéricas para escalar a media 0 y desviación estándar 1


**6. Modelado de Aprendizaje Automático**
Modelos implementados:

<img width="815" height="202" alt="image" src="https://github.com/user-attachments/assets/35c256ec-0418-410c-8c96-494750f0a1e3" />

**Configuración de entrenamiento:**
  - División de datos: 80% entrenamiento, 20% prueba (estratificada)
  - Validación cruzada: 5 folds estratificados
  - GPU: Habilitada (aceleración para XGBoost)
  - Métricas evaluadas: Accuracy, Precision, Recall, F1-Score, ROC-AUC


**7. Métricas y Evaluación de Modelos**
**Resultados en conjunto de prueba (Test Set):**

<img width="982" height="197" alt="image" src="https://github.com/user-attachments/assets/b56b0eb7-fab1-4c67-bb1a-8b826ebe4e29" />

XGBoost es el más preciso y equilibrado con un F1-Score de 0.89. Regresión Logística es de 3 a 4 veces más rápida, ideal si se prioriza latencia sobre rendimiento.

**Resultados de validación cruzada (5-Fold):**

<img width="772" height="195" alt="image" src="https://github.com/user-attachments/assets/01f51804-ed95-428b-8ab6-6369dab552a2" />

Los resultados de validación cruzada son consistentes con los del conjunto de prueba (diferencia menor al 2%), confirmando robustez y ausencia de overfitting.

**Matrices de confusión:**
  - Regresión Logística:
  - Verdaderos Negativos: 26
  - Falsos Positivos: 7
  - Falsos Negativos: 4
  - Verdaderos Positivos: 24

**Random Forest:**
  - Verdaderos Negativos: 27
  - Falsos Positivos: 6
  - Falsos Negativos: 3
  - Verdaderos Positivos: 25

**XGBoost:**
  - Verdaderos Negativos: 28
  - Falsos Positivos: 5
  - Falsos Negativos: 3
  - Verdaderos Positivos: 25

**Conclusiones rápidas por modelo:**
  - Regresión Logística: 26 verdaderos negativos y 24 verdaderos positivos. Presenta 7 falsos positivos, es decir, predice riesgo alto donde no lo hay.
  - Random Forest: Reduce los falsos positivos a 6 y los falsos negativos a 3. Mejor precisión clínica en comparación con Regresión Logística.
  - XGBoost: Mínimos errores (5 falsos positivos, 3 falsos negativos). Es el más fiable para evitar falsos negativos (pacientes de alto riesgo no detectados).


**8. Resultados y Comparativa**
**Mejor Modelo: XGBoost**

<img width="697" height="256" alt="image" src="https://github.com/user-attachments/assets/d8816dc6-7b87-4ca2-9341-734dab13db03" />

Por qué fue el mejor modelo: XGBoost combina boosting secuencial con regularización L1/L2, lo que le permite modelar relaciones no lineales complejas y evitar overfitting. Su capacidad para manejar datos tabulares mixtos (numéricos más categóricos codificados) y su optimización en GPU lo hacen superior para este dominio médico, logrando el mejor balance entre precisión y sensibilidad clínica.


**Importancia de características (Random Forest):**

<img width="847" height="306" alt="image" src="https://github.com/user-attachments/assets/982d0369-191b-4db5-aa24-e2869cfc6d40" />

El tipo de dolor de pecho es el predictor más relevante, seguido de los resultados de la prueba de talio y el número de vasos principales. Esto es clínicamente coherente: dolor asintomático junto con anomalías en talio y múltiples vasos afectados son señales críticas de alto riesgo cardiovascular. La depresión ST y la frecuencia cardíaca máxima también influyen significativamente.


**9. Conclusiones**
Hallazgos principales:
1.- XGBoost es el modelo óptimo con un accuracy del 88.5% y F1-Score de 0.89, superando a los modelos baseline.
2.- Las características más relevantes (cp, thall, caa) son clínicamente interpretables y validadas.
3.- El dataset está balanceado (54% clase 1, 46% clase 0) sin necesidad de técnicas de balanceo adicionales.
4.- La validación cruzada es consistente con el conjunto de prueba, lo que indica que no hay overfitting significativo.

**Limitaciones del estudio:**
  - Tamaño muestral reducido (303 pacientes), lo que limita la generalización de los resultados.
  - La variable fbs está muy desbalanceada (solo 15% con valores positivos).
  - No se ha realizado validación externa en una cohorte independiente.


**10. Recomendaciones para Trabajos Futuros**
**Mejoras en modelado:**
  - Ajuste de hiperparámetros: Aplicar GridSearchCV o RandomizedSearchCV para optimizar los parámetros de XGBoost y Random Forest.
  - Modelos avanzados: Experimentar con LightGBM, CatBoost o redes neuronales (MLP) para mejorar el rendimiento.
  - Ensamblaje (Stacking): Combinar los tres modelos base con un meta-modelo (ej. Regresión Logística) para potencial mejora.

**Mejoras en datos:**
  - Recolección de más datos: Incrementar el tamaño de la muestra para mejorar la generalización.
  - Balanceo de clases: Aplicar SMOTE o técnicas de sobremuestreo para clases minoritarias si es necesario.
  - Validación externa: Evaluar el modelo en un dataset diferente para confirmar robustez.

**Interpretabilidad y despliegue:**
  - SHAP values: Implementar SHAP para explicar predicciones individuales y mejorar la confianza clínica.
  - LIME: Generar explicaciones locales para cada predicción.
  - Dashboard interactivo: Desarrollar una aplicación con Streamlit o Gradio para demostración.
  - API REST: Desplegar el modelo como servicio web usando FastAPI o Flask.
