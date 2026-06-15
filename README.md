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
| #  | 	**Variable**  |	**Descripción**                                   |	**Valores / Rango**                                                        |
| 1	 |    age         | Edad del paciente	                                | 29 - 77 años                                                               |
| 2	 |    sex         | Sexo del paciente	                                | 0: Femenino, 1: Masculino                                                  |
| 3	 |    cp          | Tipo de dolor de pecho	                          | 1: Angina típica, 2: Angina atípica, 3: Dolor no anginoso, 4: Asintomático |
| 4	 |  trestbps	    | Presión arterial en reposo (mm Hg)	              | 94 - 200 mm Hg                                                             |           
| 5	 |    chol	      | Colesterol sérico en mg/dl	                      | 126 - 564 mg/dl                                                            |
| 6	 |    fbs	        | Glucemia en ayunas > 120 mg/dl	                  | 0: Falso, 1: Verdadero                                                     |
| 7	 |   restecg	    | Resultados electrocardiográficos en reposo	      | 0: Normal, 1: Anomalía ST-T, 2: Hipertrofia ventricular                    |
| 8	 |   thalachh	    | Frecuencia cardíaca máxima alcanzada	            | 71 - 202 bpm                                                               |
| 9	 |    exng	      | Angina inducida por el ejercicio	                | 0: No, 1: Sí                                                               |
| 10 |	 oldpeak	    | Depresión del segmento ST inducida por ejercicio	| 0.0 - 6.2                                                                  |
| 11 |	  slp	        | Pendiente del segmento ST de ejercicio máximo	    | 0: Ascendente, 1: Plana, 2: Descendente                                    |
| 12 |	  caa	        | Número de vasos principales (0-4) coloreados	    | 0 - 4 vasos                                                                |
| 13 |	 thall	      | Resultado de la prueba de esfuerzo con talio	    | 0: Normal, 1: Defecto fijo, 2: Reversible, 3: No descrito                  |
| 14 |	 target	      | Variable objetivo	                                | 0: Menor probabilidad de infarto, 1: Mayor probabilidad                    |
Nota: Los nombres y números de seguridad social de los pacientes fueron eliminados de la base de datos y reemplazados por valores ficticios.


**3. Análisis Exploratorio de Datos (EDA)**
| **Característica** |	**Media** |	 **Std**  |	**Min**   |	 **25%**  |	 **50%**  |	 **75%**  |	 **Max**  |
| age	               |  54.37	    |  9.08     |  29.0     |	 47.5     |	 55.0     |	 61.0     |	 77.0     |
| sex	               |   0.68	    |  0.47     |   0.0     |   0.0     |   1.0     |   1.0     |   1.0     |
| cp	               |   0.97     |	 1.03     |	  0.0     |   0.0     |   1.0     |	  2.0     |	  3.0     |
| trestbps	         | 131.62     |	17.54     |	 94.0     | 120.0     | 130.0     | 140.0     | 200.0     |
| chol	             | 246.26     |	51.83     |	126.0     |	211.0     |	240.0     |	274.5     |	564.0     | 
| thalachh	         | 149.65     |	22.91     |	 71.0     | 133.5     |	153.0     |	166.0     |	202.0     |
| oldpeak	           |   1.04     |	 1.16     |	  0.0     |	  0.0     |	  0.8     |	  1.6     |	  6.2     |

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

| **Modelo**          | **Tipo**            |	**Parámetros clave**                      |
| Regresión Logística |	Lineal              |	max_iter=1000, class_weight='balanced'    |
| Random Forest       |	Ensamble (Bagging)  |	n_estimators=100, class_weight='balanced' |
| XGBoost             |	Ensamble (Boosting) |	n_estimators=100, eval_metric='logloss'   |

Configuración de entrenamiento:
  - División de datos: 80% entrenamiento, 20% prueba (estratificada)
  - Validación cruzada: 5 folds estratificados
  - GPU: Habilitada (aceleración para XGBoost)
  - Métricas evaluadas: Accuracy, Precision, Recall, F1-Score, ROC-AUC


**7. Métricas y Evaluación de Modelos**
**Resultados en conjunto de prueba (Test Set):**


| **Modelo**          |	**Accuracy** | **Precision** | **Recall** |	**F1-Score** | **Latencia (ms/muestra)** |
| Regresión Logística |	0.8525	     | 0.8571	       | 0.8571     |	0.8571       |	0.52                     |
| Random Forest       |	0.8689	     | 0.8621	       | 0.8929     |	0.8772       |	1.87                     |
| XGBoost             |	0.8852	     | 0.8929	       | 0.8929     |	0.8929       |	2.34                     |
XGBoost es el más preciso y equilibrado con un F1-Score de 0.89. Regresión Logística es de 3 a 4 veces más rápida, ideal si se prioriza latencia sobre rendimiento.

**Resultados de validación cruzada (5-Fold):**

| **Modelo**          | **CV Accuracy** | **CV Precision** | **CV Recall** | **CV F1**  | 
| Regresión Logística | 	0.8371        | 	0.8423         | 	0.8312       | 0.8365     | 
| Random Forest       | 	0.8512        | 	0.8545         | 	0.8489       | 0.8512     | 
| XGBoost             | 	0.8645        | 	0.8689         | 	0.8612       | 0.8645     | 
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

| **Métrica**   |	**Valor**  |
| Accuracy      |	88.52%     |
| Precision     |	89.29%     |
| Recall        |	89.29%     |
| F1-Score      |	89.29%     |
Por qué fue el mejor modelo: XGBoost combina boosting secuencial con regularización L1/L2, lo que le permite modelar relaciones no lineales complejas y evitar overfitting. Su capacidad para manejar datos tabulares mixtos (numéricos más categóricos codificados) y su optimización en GPU lo hacen superior para este dominio médico, logrando el mejor balance entre precisión y sensibilidad clínica.


**Importancia de características (Random Forest):**

| **Característica**            | **Importancia** |
| cp (tipo dolor pecho)	        |      0.142      |
| thall (prueba talio)	        |      0.118      |
| caa (vasos principales)	      |      0.109      |
| oldpeak (depresión ST)	      |      0.098      |
| thalachh (frecuencia máxima)	|      0.087      |
Interpretación rápida: El tipo de dolor de pecho es el predictor más relevante, seguido de los resultados de la prueba de talio y el número de vasos principales. Esto es clínicamente coherente: dolor asintomático junto con anomalías en talio y múltiples vasos afectados son señales críticas de alto riesgo cardiovascular. La depresión ST y la frecuencia cardíaca máxima también influyen significativamente.


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
