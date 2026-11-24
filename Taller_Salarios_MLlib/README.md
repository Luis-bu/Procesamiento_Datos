# Taller de modelos de clasificación: predicción de salarios con Spark MLlib

**Autor:** Luis Ernesto Bueno Solano
**Curso:** Procesamiento de Datos a Gran Escala (código 1055) — Pontificia Universidad Javeriana
**Profesor:** John Jairo Corredor Franco, PhD
**Entrega:** 25-11-2026
**Cuaderno:** [`BuenoSalario_1055.ipynb`](BuenoSalario_1055.ipynb)

*English version below.*

## Objetivo

Construir, ajustar y comparar modelos de clasificación de Apache Spark MLlib que predigan si una persona gana más de **50 000 dólares al año**, usando los datos del censo de Estados Unidos de 1994 (dataset *Census Income / Adult* de UCI, 48 842 registros). Todo se procesa con PySpark sobre Hadoop HDFS en el clúster del curso.

## Resultados

| Modelo | AUC-ROC | AUC-PR | Accuracy | Recall (>50K) | F1 (>50K) |
|---|---|---|---|---|---|
| **GBT ajustado (umbral 0.30)** | **0.917** | **0.788** | 84.2 % | **0.810** | **0.711** |
| GBT (base) | 0.917 | 0.788 | 85.9 % | 0.628 | 0.681 |
| Random Forest | 0.913 | 0.782 | 85.6 % | 0.577 | 0.657 |
| Perceptrón multicapa | 0.904 | 0.748 | 84.8 % | 0.612 | 0.658 |
| Regresión logística | 0.901 | 0.734 | 84.5 % | 0.602 | 0.650 |
| Linear SVC | 0.898 | 0.734 | 84.6 % | 0.601 | 0.651 |
| Árbol de decisión | 0.888 | 0.752 | 84.9 % | 0.638 | 0.669 |
| Naive Bayes | 0.866 | 0.654 | 76.6 % | 0.783 | 0.616 |

*Línea base (predecir siempre `<=50K`): 76.1 % de accuracy. Conjunto de prueba: 9552 personas.*

**Hallazgos principales**
- **Conjuntos de árboles:** GBT y Random Forest superan a los modelos lineales porque capturan interacciones entre variables (por ejemplo, edad × educación). El bootstrap confirma que GBT supera a Random Forest (+0.004 de AUC, IC 95 % [0.002, 0.006]).
- **Umbral de decisión:** la validación cruzada casi no cambió el AUC. Bajar el umbral a 0.30, elegido en un conjunto de validación, subió el recall de 63 % a 81 % y el F1 de 0.68 a 0.71.
- **Variables más importantes:** edad, educación, ocupación, rol en el hogar o estado civil, y capital.
- **Equidad:** el modelo detecta peor a las mujeres con ingresos altos (recall 0.73 frente a 0.82); hay que corregirlo antes de usarlo en decisiones sobre personas.

## Contenido del cuaderno

Las secciones siguen el orden de la rúbrica del taller:

| Sección | Contenido |
|---|---|
| Presentación | Identificación, resumen ejecutivo, *abstract*, contexto, comprensión del negocio (CRISP-DM), criterios de éxito y objetivos |
| 1. Carga de datos en HDFS | Subida de `adult.data` y `adult.test` a HDFS y lectura con esquema explícito |
| 2. EDA general | Diccionario de datos, variable objetivo, estadísticas, categorías, 8 gráficas de relación con el ingreso, correlaciones e interacción edad × educación |
| 3. Preparación de datos: análisis y gráficas | Faltantes, duplicados, variables redundantes, categorías raras, atípicos y asimetría, con una tabla problema → evidencia → decisión |
| 4. Tratamiento de datos y pipeline | Limpieza con gráficas antes/después, división 80/20 reproducible y `Pipeline` de 12 etapas ajustado solo con entrenamiento |
| 5. Aplicación de modelos MLlib | 7 modelos base, `CrossValidator` para GBT y regresión logística, umbral elegido en validación y modelo final guardado en HDFS |
| 6. Comparativa general | Ranking, curvas ROC y PR, matrices de confusión, intervalos de confianza por bootstrap, costo vs. desempeño, importancia de variables y desempeño por sexo y raza |
| 7. Conclusiones y recomendaciones | Cumplimiento de objetivos y criterios, conclusiones, recomendaciones por caso de uso, trabajo futuro y limitaciones |
| 8. English summary | Resumen en inglés |

## Cómo ejecutarlo

**En el clúster del curso (como se entregó):**
1. Tomar `adult.data` y `adult.test` de la carpeta [`data/`](data/) (o del zip oficial de UCI).
2. Subir el cuaderno y los dos archivos a la misma carpeta de Jupyter.
3. Abrir el cuaderno con el kernel `rapKernel_v4` y ejecutar todas las celdas. Las primeras celdas copian los datos a HDFS (`/Formatos1055/BuenoLuis/Salario`) y la sección 5.5 guarda allí el modelo final.

**Fuera del clúster:** instalar `requirements.txt` y Java 11 o 17. Hay que ajustar `findspark.init(...)` a la ruta local de Spark, cambiar las rutas `hdfs://...` por rutas locales y omitir las celdas `!hadoop`.

---

## English version

**Goal.** Build, tune and compare Apache Spark MLlib classifiers that predict whether a person earns more than **USD 50,000 per year**, using the 1994 US Census data (UCI *Census Income / Adult*, 48,842 records). Everything runs on PySpark over Hadoop HDFS on the course cluster.

**Results.** The **tuned GBT** (100 trees, depth 4, decision threshold 0.30) is the best model, with **ROC-AUC 0.917, PR-AUC 0.788, recall 0.81 and F1 0.711** on the test set. The majority-class baseline is 76.1 % accuracy.

**Key findings.**
- Tree ensembles beat linear models because they capture interactions between variables, such as age × education.
- Most of the improvement came from tuning the decision threshold on a validation set, not from the hyperparameters.
- Age, education, occupation, household role and capital gains are the strongest predictors.
- The model has lower recall for women (0.73 vs 0.82), which must be addressed before using it for decisions about people.

**Notebook outline.**
- Data loading into HDFS.
- Exploratory analysis.
- Data quality diagnosis with charts.
- Data treatment and a feature `Pipeline` fitted on training data only.
- Seven MLlib models, plus `CrossValidator` tuning and threshold selection.
- Model comparison with bootstrap confidence intervals and a fairness check.
- Conclusions and recommendations, and an English summary.

The final `PipelineModel` is saved to HDFS and reloaded with identical predictions.

**Data source:** Kohavi, R. (1996). *Census Income* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5GP7S (CC BY 4.0).
