# Análisis de datos sobre el Infarto de Miocardio

Este repositorio contiene la exploración y el análisis de un conjunto de datos clínicos relacionado con infartos de miocardio (IM). 
El objetivo es **comprender** las variables más relevantes y **experimentar** con distintos métodos de minería de datos para detectar patrones y predecir posibles complicaciones.

## 1. Estructura del Proyecto

- **data/**  
  - Contiene el archivo original `myocardial_infarctation.CSV` y el dataset limpio `IM.csv`.

- **scripts/**  
  - `exploracion_inicial.Rmd`:  
    - Carga y descripción del dataset.
    - Limpieza (eliminación de variables muy incompletas) e imputación (KNN, media, moda).
    - Visualizaciones iniciales (histogramas, boxplots, PCA) y generación de `IM.csv`.
  - `analisis_no_supervisado.Rmd`:  
    - Análisis de clustering (K-means, PAM, DBSCAN, OPTICS) con evaluación mediante el método del codo, silhouette, Calinski-Harabasz, entre otros.
    - Interpretación de clusters y discusión sobre las limitaciones.
  - `analisis_supervisado.Rmd`:  
    - Modelos predictivos (árboles de decisión, boosting y random forest) para predecir la variable **LET_IS**.
    - Uso de SMOTE para balancear las clases.
    - Evaluación mediante precisión, matrices de confusión y curvas ROC.
    
- **README.md**  
  - Este archivo, que contiene la descripción general del proyecto, requisitos e instrucciones para reproducir el análisis.
  

## 2. Requisitos y Dependencias

Para reproducir correctamente los análisis, se requieren los siguientes paquetes de R:

- `dplyr`
- `ggplot2`
- `tidymodels`
- `recipes`
- `arules`
- `tidyr`
- `stats`
- `caret`
- `C50`
- `randomForest`
- `smotefamily`
- `pROC`
- `gmodels`
- `DescTools`
- `gridExtra`
- `iml`

> Puedes instalarlos con:
> ```r
> install.packages(c("dplyr", "ggplot2", "tidymodels", "recipes", "arules",
>                    "tidyr", "stats", "caret", "C50", "randomForest",
>                    "smotefamily", "pROC", "gmodels", "DescTools", "gridExtra", "iml"))
> ```

Se recomienda utilizar **R 4.0 o superior**. Para una mayor reproducibilidad, se puede utilizar un entorno virtual con [**renv**](https://rstudio.github.io/renv/).

## 3. Cómo Reproducir el Proyecto

1. **Clona** este repositorio o descarga su contenido.
2. Coloca el archivo de datos original `myocardial_infarctation.CSV` en la carpeta `data/` (si aún no está allí).
3. Abre los archivos `.Rmd` en RStudio (o el editor de tu preferencia) y ejecútalos en el siguiente orden:
   - **`exploracion_inicial.Rmd`**:  
     - Realiza la limpieza y la imputación, generando el dataset `IM.csv` limpio.
   - **`analisis_no_supervisado.Rmd`**:  
     - Carga `IM.csv` y realiza el análisis de clustering, interpretando los resultados y evaluando la cohesión de los clusters.
   - **`analisis_supervisado.Rmd`**:  
     - Carga `IM.csv` y entrena modelos predictivos con técnicas de balanceo (SMOTE), evaluando el desempeño y discutiendo las limitaciones.
4. Si deseas ver los resultados sin ejecutar el código, compila cada archivo a **HTML** usando la función “Knit” en RStudio y comparte esos archivos.

## 4. Descripción General del Dataset

El conjunto de datos contiene información clínica de pacientes con infarto de miocardio, la cual abarca:

- **Variables demográficas**: Edad, sexo.
- **Antecedentes cardíacos**: Infartos previos, angina, arritmias, hipertensión.
- **Patologías de otros sistemas**: Diabetes, obesidad, bronquitis, asma, entre otras.
- **Parámetros de laboratorio**: Niveles de potasio, sodio, enzimas cardíacas y recuento de células blancas.
- **Complicaciones**: Incluye arritmias, edema pulmonar, ruptura miocárdica, reinfarto, etc.
- **Resultado letal**: La variable `LET_IS` codifica distintos desenlaces (0: desconocido/vivo, 1: shock cardiogénico, etc.).

El desbalance de clases es significativo, lo que influye en la capacidad de los modelos para predecir las complicaciones menos frecuentes.

## 5. Hallazgos y Limitaciones

- **Exploración Inicial**:  
  Se limpiaron y transformaron los datos mediante la eliminación de variables muy incompletas y la imputación (KNN, media, moda).  
  Se observaron patrones en variables de laboratorio y se identificó un alto porcentaje de valores faltantes en algunos parámetros.

- **Análisis No Supervisado**:  
  Los métodos de clustering (K-means, PAM, DBSCAN, OPTICS) no lograron identificar clusters robustos y clínicamente diferenciados, posiblemente debido a la alta variabilidad y desbalance del dataset.

- **Análisis Supervisado**:  
  Aunque los modelos (árboles de decisión, boosting y random forest) muestran altos niveles de precisión global, se detecta una baja sensibilidad para las clases minoritarias, lo que limita su aplicabilidad en entornos clínicos.  
  Las técnicas de balanceo (SMOTE) mejoraron ligeramente el desempeño, pero persiste un sesgo hacia la clase mayoritaria.

- **Aplicabilidad Clínica**:  
  Debido al desbalance y a la variabilidad en los desenlaces críticos, los modelos actuales requieren mejoras importantes antes de poder aplicarse en la práctica médica.

## 6. Licencia



## 7. Créditos y Referencias

- **Fuente de datos**:  
  - [UCI Machine Learning Repository – Infarto de Miocardio](https://archive.ics.uci.edu/dataset/579/myocardial+infarction+complications)  
  - DOI: [10.25392/leicester.data.12045261.v3](https://doi.org/10.25392/leicester.data.12045261.v3)

- **Autor**: Javier Gazquez Garcia

- Gracias a la comunidad open-source y a los desarrolladores de los paquetes de R que hacen posible este análisis.
