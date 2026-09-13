# Credit Scoring con German Credit Data

Prototipo reproducible de **Credit Scoring** desarrollado en Python utilizando **Regresión Logística** y **Random Forest** sobre el conjunto de datos **German Credit Data**.

El proyecto forma parte del proyecto final de la materia de seminario de innovación en análisis y visualización de datos orientado a demostrar cómo una metodología de análisis y modelado predictivo puede integrarse en una herramienta funcional capaz de evaluar nuevos solicitantes, generar probabilidades de riesgo y presentar una clasificación crediticia de forma comprensible.

## Objetivo

Construir un prototipo que permita:

- procesar información de nuevos solicitantes;
- aplicar automáticamente las transformaciones requeridas por los modelos;
- ejecutar modelos de Regresión Logística y Random Forest;
- estimar la probabilidad de pertenencia a la clase `Bad`;
- aplicar umbrales de decisión específicos para cada modelo;
- presentar una clasificación `Good` o `Bad`;
- generar un resultado de consenso entre ambos modelos;
- reproducir las evaluaciones sin necesidad de entrenar nuevamente los modelos en cada sesión.

## Conjunto de datos

Se utiliza el conjunto **German Credit Data (Statlog)**, compuesto por:

- 1,000 observaciones;
- 20 variables predictoras;
- una variable objetivo binaria;
- aproximadamente 70 % de registros clasificados como `Good` y 30 % como `Bad`.

En la implementación del prototipo, la clase positiva corresponde a `Bad`, por lo que las probabilidades reportadas representan la probabilidad estimada de pertenecer a dicha clase.

## Modelos incluidos

### Regresión Logística

El modelo utiliza ocho variables seleccionadas a partir del análisis previo de relevancia:

- estado de la cuenta corriente;
- historial crediticio;
- duración del crédito;
- estado de la cuenta de ahorro;
- propósito del crédito;
- monto solicitado;
- tiempo de residencia;
- tipo de propiedad.

El umbral operativo utilizado en el prototipo es **0.50**.

### Random Forest

El modelo utiliza las 20 variables predictoras disponibles. Las variables numéricas y categóricas son procesadas mediante un pipeline que incluye estandarización y One-Hot Encoding.

El modelo fue optimizado mediante Grid Search y validación cruzada. La configuración seleccionada utiliza:

- `n_estimators = 500`
- `max_depth = 10`
- `max_features = sqrt`
- `criterion = gini`

El umbral operativo utilizado en el prototipo es **0.55**.

## Validación del prototipo

En la implementación reproducible del prototipo se obtuvo:

| Modelo | ROC-AUC | Gini |
|---|---:|---:|
| Regresión Logística | 0.7795 | 0.5589 |
| Random Forest optimizado | 0.7786 | 0.5572 |

La diferencia entre ambos modelos fue reducida, por lo que el prototipo conserva los dos clasificadores y presenta sus resultados de manera conjunta.

## Flujo de funcionamiento

El prototipo sigue el siguiente proceso:

1. Captura de las 20 características del solicitante.
2. Validación de la estructura del registro.
3. Transformación automática mediante los pipelines previamente ajustados.
4. Generación de probabilidades mediante Regresión Logística y Random Forest.
5. Aplicación de los umbrales de decisión.
6. Obtención de clasificaciones individuales.
7. Generación de un resultado de consenso.
8. Presentación numérica y gráfica de los resultados.

## Interfaz interactiva

El notebook incluye una interfaz desarrollada con `ipywidgets` que permite capturar la información de un nuevo solicitante sin modificar directamente el código.

Las variables categóricas se presentan mediante listas descriptivas y las variables cuantitativas mediante controles numéricos. Al seleccionar **Evaluar solicitante**, el prototipo ejecuta automáticamente ambos modelos y presenta:

- probabilidad estimada de clase `Bad`;
- umbral de decisión;
- clasificación de cada modelo;
- consenso entre modelos;
- visualización comparativa de los resultados.

## Modos de ejecución

El proyecto contempla dos formas de utilización.

### Modo de desarrollo

Permite reproducir el proceso completo de preparación, entrenamiento, optimización y evaluación de los modelos.

### Modo operativo

Permite cargar los modelos previamente entrenados y evaluar nuevos solicitantes sin ejecutar nuevamente las etapas de entrenamiento o Grid Search.

En una sesión nueva de Jupyter Notebook, el flujo operativo consiste en:

1. cargar las bibliotecas, modelos y configuración almacenada;
2. inicializar los datos y catálogos utilizados por la interfaz;
3. ejecutar las funciones de validación y evaluación;
4. cargar la interfaz interactiva;
5. capturar los datos del solicitante y ejecutar la evaluación.

## Estructura esperada del repositorio

```text
credit-scoring-german-data/
│
├── PROTOTIPO_CREDIT_SCORING.ipynb
├── german.csv
├── modelo_regresion_logistica.pkl
├── modelo_random_forest_optimizado.pkl
├── configuracion_prototipo.pkl
├── resultado_credit_scoring_demo.csv
├── README.md
├── requirements.txt
└── .gitignore
```

## Tecnologías utilizadas

- Python
- Pandas
- NumPy
- scikit-learn
- imbalanced-learn
- Matplotlib
- Seaborn
- ipywidgets
- Jupyter Notebook
- Pickle

## Reproducibilidad

Los modelos y la configuración del prototipo se almacenan mediante serialización, permitiendo recuperarlos en sesiones posteriores sin repetir el entrenamiento. Durante las pruebas se verificó que las probabilidades y clasificaciones obtenidas después de guardar y volver a cargar los modelos fueran idénticas a las generadas originalmente.

El flujo de validación mantiene separado el conjunto de prueba antes de aplicar sobremuestreo y restringe el balanceo de clases al proceso de entrenamiento. El ROC-AUC se calcula a partir de las probabilidades generadas por los clasificadores.

## Alcance

Este proyecto corresponde a un **prototipo demostrativo**. No constituye un sistema de aprobación o rechazo de crédito listo para utilizarse en un entorno financiero real.

Una implementación productiva requeriría, entre otros elementos, validación con datos actuales y representativos de la población objetivo, revisión de variables y criterios de negocio, gobierno y monitoreo del modelo, controles de seguridad y cumplimiento de los requisitos regulatorios aplicables.

## Autores

Proyecto desarrollado por el **Equipo 2_C** como parte de la maestría en Análisis y Visualización de Datos Masivos.

## Fuente de datos

German Credit Data / Statlog German Credit Data, UCI Machine Learning Repository.
