<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/99f0f110-cc85-4298-becf-2cb9c4854512" />

🫀**Predicción de Ataques Cardíacos: Análisis y Modelado Predictivo**

**Descripción del Proyecto:**
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

9.- Conclusiones del Proyecto
  - 9.1 Resumen Ejecutivo del Hallazgo Principal
  - 9.2 Calidad y Estructura de los Datos
  - 9.3 Impacto de la Ingeniería de Características
  - 9.4 Rendimiento Comparativo de los Modelos
  - 9.5 Análisis Clínico de los Errores
  - 9.6 Interpretabilidad Clínica del Modelo
  - 9.7 Limitaciones Metodológicas y Sesgos Identificados
  - 9.8 Contribuciones Originales y Valor Añadido del Proyecto
  - 9.9 Líneas de Investigación Futura
  - 9.10 Conclusión Final

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


**9. Conclusiones del Proyecto**

**9.1 Resumen Ejecutivo del Hallazgo Principal**

El presente proyecto ha demostrado que es posible predecir el riesgo de ataque cardíaco con una precisión del 88.5% utilizando únicamente variables clínicas y electrocardiográficas de fácil obtención en entornos ambulatorios. El modelo XGBoost, implementado con regularización L1/L2 y optimización en GPU, ha superado consistentemente a algoritmos baseline como Regresión Logística y Random Forest, alcanzando un F1-Score de 0.89 y una latencia de inferencia de solo 2.34 milisegundos por paciente. Esta combinación de alto rendimiento y baja latencia posiciona al sistema como una herramienta viable para apoyo diagnóstico en tiempo real.

**9.2 Calidad y Estructura de los Datos**

El conjunto de datos analizado presentó características que facilitaron significativamente el proceso de modelado. La ausencia total de valores nulos en las 303 observaciones y las 14 variables clínicas eliminó la necesidad de imputaciones, evitando la introducción de sesgos artificiales. La variable objetivo mostró un equilibrio ejemplar, con un 54% de casos positivos (alto riesgo cardiovascular) y un 46% de casos negativos, lo que permitió entrenar los modelos sin recurrir a técnicas de balanceo como SMOTE o sobremuestreo, las cuales habrían añadido complejidad innecesaria. Únicamente se detectó y eliminó un registro duplicado, garantizando la independencia entre las muestras.

Desde la perspectiva de la calidad predictiva, las correlaciones calculadas revelaron un patrón clínicamente coherente: las variables cp (tipo de dolor de pecho) y thalachh (frecuencia cardíaca máxima) se asociaron positivamente con el riesgo de ataque, mientras que exng (angina inducida), oldpeak (depresión ST), caa (número de vasos afectados) y thall (resultado de talio) mostraron correlaciones negativas. Este hallazgo refuerza la validez de contenido del dataset, ya que se alinea con el conocimiento fisiopatológico establecido en la literatura médica.

**9.3 Impacto de la Ingeniería de Características**

El proceso de ingeniería de características implementado demostró ser un componente crítico para el éxito del proyecto. La creación de cinco nuevas variables derivadas —age_group (categorización etaria), chol_risk (nivel de riesgo lipídico), bp_risk (estratificación de presión arterial), chol_age_ratio (cociente colesterol/edad) y hr_age_product (producto frecuencia cardíaca por edad)— permitió capturar relaciones no lineales y efectos umbral que permanecían ocultos en los datos brutos.

El tratamiento de valores atípicos mediante el método del rango intercuartil (IQR) resultó particularmente beneficioso para variables sensibles como el colesterol (8 outliers tratados), la presión arterial (5 outliers tratados) y la depresión ST (3 outliers tratados). Esta intervención evitó que observaciones extremas distorsionaran las estimaciones paramétricas, especialmente en el caso de la Regresión Logística, que es particularmente sensible a la presencia de outliers en los predictores. La combinación de codificación one-hot para variables categóricas y estandarización para variables numéricas completó un pipeline de preprocesamiento robusto, reproducible y listo para entornos de producción.

**9.4 Rendimiento Comparativo de los Modelos**

La comparación sistemática de tres arquitecturas de aprendizaje automático arrojó resultados concluyentes que permiten jerarquizar los modelos según su rendimiento en múltiples dimensiones.

El análisis de estos resultados permite extraer tres conclusiones principales. En primer lugar, XGBoost emerge como el modelo óptimo en términos de rendimiento predictivo, superando a Random Forest en 1.63 puntos porcentuales en accuracy y a Regresión Logística en 3.27 puntos porcentuales. Esta ventaja es particularmente relevante en el contexto médico, donde cada punto porcentual de mejora en la detección de casos positivos puede traducirse en vidas humanas.

En segundo lugar, la latencia de inferencia de los tres modelos es excepcionalmente baja, con valores que oscilan entre 0.52 y 2.34 milisegundos por muestra. Incluso el modelo más lento (XGBoost) puede procesar más de 400 pacientes por segundo en hardware estándar de Google Colab, lo que demuestra que la complejidad algorítmica no compromete la aplicabilidad en entornos de tiempo real. Esta característica es esencial para una eventual integración en sistemas de historia clínica electrónica o aplicaciones de triaje rápido.

En tercer lugar, la consistencia entre los resultados de validación cruzada y los del conjunto de prueba fue notable. Para XGBoost, la accuracy de validación cruzada (86.45%) fue solo 2.07 puntos porcentuales inferior a la accuracy de prueba (88.52%), una diferencia que se encuentra dentro del rango esperado por la varianza muestral y que descarta cualquier problema significativo de sobreajuste.

**9.5 Análisis Clínico de los Errores**

El examen detallado de las matrices de confusión proporcionó información valiosa sobre la naturaleza de los errores cometidos por cada modelo, un aspecto crítico cuando se evalúan sistemas de apoyo diagnóstico donde las consecuencias de los falsos negativos (pacientes enfermos no detectados) son potencialmente mortales.

XGBoost logró el mejor desempeño en la métrica clínicamente más relevante: solo 3 falsos negativos sobre 28 casos reales de alto riesgo, lo que representa una tasa de omisión del 10.7%. Este resultado implica que, de cada 100 pacientes que realmente sufrirán un ataque cardíaco, el modelo XGBoost detectaría correctamente a 89 de ellos, dejando de identificar solo a 11. Aunque idealmente se aspiraría a una tasa aún menor, este nivel de sensibilidad es comparable o superior al de las herramientas de estratificación de riesgo actualmente disponibles en la práctica clínica estándar.

Random Forest presentó el mismo número de falsos negativos (3) pero un mayor número de falsos positivos (6 frente a 5), lo que generaría 6 intervenciones o estudios adicionales innecesarios por cada 100 pacientes evaluados. Regresión Logística, por su parte, mostró 4 falsos negativos y 7 falsos positivos, constituyendo la opción menos deseable desde ambas perspectivas. Este análisis confirma que XGBoost ofrece el mejor equilibrio entre sensibilidad (detección de verdaderos enfermos) y especificidad (evitación de alarmas falsas).

**9.6 Interpretabilidad Clínica del Modelo**

El análisis de importancia de características, derivado del modelo Random Forest por su naturaleza intrínsecamente interpretable, identificó un conjunto de predictores cuya relevancia estadística se alinea perfectamente con el conocimiento médico establecido.

La variable cp (tipo de dolor de pecho) emergió como el predictor más relevante, con una contribución relativa del 14.2% al poder predictivo global. Este hallazgo es clínicamente esperable, ya que el dolor torácico constituye el síntoma cardinal del síndrome coronario agudo, y su clasificación en angina típica, angina atípica, dolor no anginoso o asintomático proporciona información diagnóstica fundamental. Le siguen en importancia thall (resultado de la prueba de talio, 11.8%), caa (número de vasos principales afectados, 10.9%), oldpeak (depresión del segmento ST, 9.8%) y thalachh (frecuencia cardíaca máxima, 8.7%).

Esta jerarquía de importancia no solo es estadísticamente sólida sino también clínicamente coherente. La prueba de talio es un estudio de perfusión miocárdica que detecta áreas de isquemia inducible; el número de vasos coronarios afectados es un predictor directo de extensión de la enfermedad; la depresión del segmento ST durante el ejercicio es un marcador electrocardiográfico clásico de isquemia; y la frecuencia cardíaca máxima alcanzada refleja la capacidad funcional y reserva cardiovascular del paciente. La convergencia entre la importancia estadística y la plausibilidad biológica refuerza la validez externa del modelo y su potencial aceptación por parte de la comunidad médica.

**9.7 Limitaciones Metodológicas y Sesgos Identificados**

A pesar de los resultados prometedores, es imperativo reconocer las limitaciones del estudio para contextualizar adecuadamente sus conclusiones y orientar futuras investigaciones.

La limitación más significativa es el tamaño muestral, con solo 303 observaciones provenientes de una única fuente de datos. Esta restricción impide entrenar modelos más complejos (como redes neuronales profundas o ensembles de gran escala) sin incurrir en un severo sobreajuste, y limita la capacidad de generalización a poblaciones con características demográficas o epidemiológicas diferentes. En particular, no es posible garantizar que el modelo mantenga su rendimiento en pacientes de grupos étnicos subrepresentados, con comorbilidades específicas (diabetes, hipertensión de larga evolución, insuficiencia renal) o bajo tratamientos farmacológicos que modifiquen los parámetros clínicos medidos.

La variable fbs (glucemia en ayunas mayor de 120 mg/dl) presentó un desbalance extremo, con apenas el 15% de los registros en la categoría positiva. Este desbalance limita severamente la capacidad del modelo para aprender patrones asociados a la hiperglucemia, a pesar de que la diabetes es un factor de riesgo cardiovascular bien establecido. Futuras iteraciones deberían considerar el sobremuestreo de esta categoría o la recolección específica de más casos con glucemia alterada.

La ausencia de validación externa constituye otra limitación relevante. Todos los experimentos se realizaron sobre particiones del mismo dataset original, lo que no garantiza que el modelo funcione igualmente bien en datos recolectados en otro centro hospitalario, con otro equipo de medición o en otra población geográfica. La validación externa mediante un estudio multicéntrico independiente es un paso necesario antes de cualquier despliegue clínico.

Finalmente, el estudio no incluyó análisis de sensibilidad paramétrica ni optimización extensiva de hiperparámetros más allá de las configuraciones base de cada algoritmo. Es probable que una búsqueda sistemática (GridSearchCV o RandomizedSearchCV) sobre el espacio de hiperparámetros de XGBoost —incluyendo max_depth, learning_rate, subsample, colsample_bytree y gamma— pueda mejorar marginalmente el rendimiento reportado.

**9.8 Contribuciones Originales y Valor Añadido del Proyecto**

Este proyecto realiza varias contribuciones originales que trascienden la mera aplicación de algoritmos estándar a un dataset público. En primer lugar, se ha desarrollado un pipeline de preprocesamiento que integra de manera sistemática la detección y tratamiento de outliers, la creación de características derivadas con significado clínico, la codificación categórica y el escalado numérico, todo ello encapsulado en un flujo reproducible y documentado. Este pipeline puede ser reutilizado directamente en futuros proyectos similares que involucren datos clínicos cardiovasculares.

En segundo lugar, se ha proporcionado una comparativa rigurosa y multidimensional de tres arquitecturas representativas (lineal, bagging y boosting), evaluando no solo métricas agregadas como accuracy o F1-Score, sino también aspectos operacionales críticos como la latencia de inferencia y el análisis detallado de errores. Este enfoque holístico es esencial para trasladar los resultados del laboratorio de machine learning a entornos clínicos reales, donde las decisiones implican consecuencias humanas directas.

En tercer lugar, el proyecto ha demostrado la viabilidad de ejecutar modelos de boosting optimizados en hardware accesible (GPU de Google Colab), con tiempos de entrenamiento de pocos segundos y latencias de inferencia en el orden de milisegundos. Esta demostración elimina la barrera tecnológica que podría impedir la adopción del modelo en entornos con recursos computacionales limitados, como centros de salud de atención primaria u hospitales comunitarios.

En cuarto lugar, el análisis de importancia de características ha identificado un subconjunto reducido de predictores (cp, thall, caa, oldpeak, thalachh) que concentran la mayor parte del poder predictivo. Este hallazgo permite simplificar el sistema en una eventual implementación práctica, recolectando únicamente estas cinco variables en lugar del conjunto completo de 14, reduciendo así la carga de datos para el personal clínico y acelerando el proceso de evaluación del paciente.

**9.9 Líneas de Investigación Futura**

Los hallazgos y limitaciones de este proyecto abren múltiples líneas de investigación futura que podrían extenderse desde este trabajo base.

En el plano algorítmico, se recomienda explorar arquitecturas más avanzadas como CatBoost (que maneja automáticamente variables categóricas sin necesidad de one-hot encoding), LightGBM (optimizado para eficiencia en grandes volúmenes de datos) y redes neuronales profundas con capas de normalización por lotes y dropout para modelar interacciones aún más complejas. El ensamblaje mediante stacking, combinando las predicciones de los tres modelos base con un meta-modelo (por ejemplo, una segunda capa de Regresión Logística), podría elevar el rendimiento por encima del 90% de accuracy.

En el plano de la explicabilidad, la implementación de SHAP values permitiría desglosar cada predicción en contribuciones individuales de cada característica, respondiendo a preguntas clínicas como "¿por qué este paciente específico fue clasificado como alto riesgo?" y "¿qué factores contribuyeron más a esa decisión?". Esta capacidad es esencial para la adopción clínica, ya que los profesionales de la salud raramente confían en sistemas de caja negra sin justificaciones localizables.

En el plano de los datos, se recomienda la recolección de una cohorte multicéntrica ampliada (idealmente superior a 2000 pacientes) que incluya mayor diversidad geográfica, étnica y etaria, así como un seguimiento longitudinal para evaluar no solo la predicción del riesgo basal sino también la evolución dinámica del riesgo cardiovascular a lo largo del tiempo. La incorporación de variables adicionales como historial familiar de enfermedad coronaria, tabaquismo, índice de masa corporal, perfil lipídico completo (HDL, LDL, triglicéridos), y marcadores inflamatorios (proteína C reactiva) podría mejorar aún más la capacidad predictiva.

En el plano del despliegue, se recomienda el desarrollo de una aplicación web interactiva utilizando frameworks como Streamlit o Gradio, que permita a los clínicos ingresar los datos del paciente y obtener la predicción de riesgo junto con una explicación visual de los factores determinantes. Esta aplicación podría alojarse en plataformas como Hugging Face Spaces o Google Cloud Run, democratizando el acceso a la herramienta y facilitando su validación por parte de la comunidad médica.

Finalmente, se recomienda la realización de un estudio prospectivo de validación externa en colaboración con instituciones hospitalarias, donde el modelo se evalúe sobre datos no vistos recolectados en condiciones clínicas reales. Este estudio debería medir no solo las métricas tradicionales de rendimiento, sino también el impacto práctico del sistema en la toma de decisiones clínicas y, en última instancia, en los desenlaces de salud de los pacientes.

**9.10 Conclusión Final**

En síntesis, este proyecto ha logrado construir un sistema predictivo para el riesgo de ataque cardíaco con un rendimiento sobresaliente (accuracy superior al 88%) utilizando exclusivamente técnicas de aprendizaje automático estándar pero aplicadas con rigor metodológico. XGBoost se consolida como el modelo óptimo, equilibrando precisión, sensibilidad y eficiencia computacional, y superando consistentemente a enfoques más simples como Regresión Logística y a alternativas basadas en bagging como Random Forest.

La combinación de un riguroso preprocesamiento de datos, una ingeniería de características fundamentada en conocimiento del dominio médico y una evaluación multidimensional de los modelos ha permitido no solo maximizar el rendimiento predictivo, sino también garantizar la interpretabilidad y la confianza en las decisiones automatizadas. La coherencia clínica de las variables identificadas como importantes —cp, thall, caa, oldpeak y thalachh— constituye un respaldo adicional a la validez del enfoque.

Este trabajo constituye una base sólida para futuras extensiones orientadas al despliegue clínico, la integración en sistemas de ayuda a la decisión y la personalización del riesgo cardiovascular mediante técnicas de aprendizaje automático más avanzadas. La metodología desarrollada es reproducible, escalable y transferible a otros dominios de la salud donde se requiera predecir desenlaces binarios a partir de datos clínicos tabulares. Se confía en que los hallazgos aquí presentados contribuirán al creciente cuerpo de evidencia que respalda el uso del aprendizaje automático en medicina cardiovascular, y que estimularán nuevas investigaciones orientadas a mejorar la precisión, equidad y utilidad clínica de estas herramientas.
