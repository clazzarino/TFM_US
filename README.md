# Master Universitario en Ingeniería Biomédica y Salud Digital de la Universidad de Sevilla
# Trabajo de Fin de Master

# 🦟 Machine Learning para la Predicción de la Propagación del Dengue

## Descripción del Proyecto
Este proyecto presenta el diseño, desarrollo y validación de un sistema predictivo basado en Machine Learning para anticipar la propagación del dengue en entornos urbanos y selváticos. A partir del desafío DengAI de DrivenData, el modelo propone una transición hacia una epidemiología predictiva utilizando datos climáticos y satelitales (NOAA y CDC) de las ciudades de San Juan (Puerto Rico) e Iquitos (Perú). A través de un procesamiento enriquecido de los datos, el algoritmo traduce la biología del vector *Aedes aegypti* a variables matemáticas.

## DengAI:
DrivenData. (2016). DengAI: Predicting Disease Spread. Retrieved from https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/.

## Arquitectura y Metodología
El flujo de trabajo contrasta el rendimiento de tres arquitecturas:

1. **LightGBM (Gradient Boosting):** Algoritmo principal que demostró superioridad frente a los datos tabulares ruidosos, ofreciendo el mejor equilibrio de generalización.
2. **Máquinas de Vectores de Soporte (SVM):** Implementación geométrica (Radial Kernel) optimizada mediante Grid Search.
3. **Redes Neuronales Artificiales (MLP con Torch)**: Implementación en R utilizando `libtorch` y `luz`, para modelar dependencias no lineales complejas. Las variables predictoras se estandarizan (z-score) con parámetros calculados sobre el entrenamiento, y la variable objetivo se transforma con `log1p` para comprimir los picos epidémicos. Los hiperparámetros se optimizan de forma independiente para cada ciudad, con validación temporal y pérdida MSE.

### Feature Engineering Biológico
Para capturar los tiempos biológicos del vector, el pipeline incorpora:
* **Retardos temporales (Lags) y Deltas:** Simulando el periodo de incubación intrínseco y extrínseco.
* **Promedios Móviles y Estacionalidad:** Extracción de ruido en series temporales meteorológicas.
* **Imputación Direccional (LOCF):** Estabilización de mediciones ambientales sin ruptura de la línea temporal.

## Tecnologías y Dependencias
El ecosistema de desarrollo se basa íntegramente en herramientas Open Source. Para ejecutar el entorno de experimentación en R, se requieren las siguientes librerías:

* `data.table` (Manejo eficiente de grandes volúmenes de datos)
* `lightgbm` (Implementación del ensamble de árboles)
* `e1071` (Para algoritmos SVM)
* `torch` y `luz` (Ecosistema de Deep Learning sin dependencias de Python)
* `rBayesianOptimization` (Ajuste avanzado de hiperparámetros)
* `zoo` (Para imputaciones de valores de series temporales)

## Uso e Implementación
1. Clonar el repositorio.
2. Asegurar que los datasets brutos (`dengue_features_train.csv`, `dengue_labels_train.csv`, `dengue_features_test.csv`) se encuentren en la misma ruta de trabajo.
3. Ejecutar el cuaderno principal (`TFM_US_Lazzarino.ipynb`).
4. En su primera ejecución, el script descargará el backend C++ para Torch (`libtorch`, ~1.5GB) e iniciará la Optimización Bayesiana. Los mejores hiperparámetros se guardarán localmente en archivos `.txt` para acelerar futuras ejecuciones. Si el archivo .txt existe, toma esos valores.
5. Las salidas finales en formato Submission se validarán automáticamente para verificar su integridad y se guardan en formato `.csv`.

## Visión y Salud Digital
Más allá del reto analítico, el diseño modular de este trabajo sienta las bases para futuras implementaciones en Informática Médica. La integración de los resultados de estos modelos bajo estándares internacionales de interoperabilidad técnica (como **HL7 FHIR**) permitiría automatizar alertas tempranas en Sistemas de Información Hospitalaria, optimizando la respuesta de las redes de salud locales ante emergencias sanitarias.

# Data:
Submission_Format.csv
Formato en el que se realizan los submit a la competencia

dengue_features_test.csv
Features para el dataset de testeo.

dengue_features_train.csv
Features para el dataset de entrenamiento.

dengue_labels_train.csv
Numero de casos para cada una de las filas del dataset de entrenamiento.



