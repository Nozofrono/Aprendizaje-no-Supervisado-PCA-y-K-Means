# Reporte de Experimento: Aprendizaje No Supervisado en Calidad de Vino

## 1. Introducción
Este reporte documenta el análisis de aprendizaje no supervisado realizado sobre el dataset **Wine Quality** tomado de kaggle.com. El trabajo se enfoca en la reducción de dimensionalidad mediante PCA y la segmentación de datos utilizando el algoritmo de agrupamiento K-Means.

## 2. Metodología

### 2.1. Preparación de Datos
Se utilizó una muestra fisicoquímica de vinos, eliminando identificadores y asegurando la integridad del dataset. Debido a que algoritmos como PCA y K-Means son sensibles a las escalas de las variables, se aplicó una **Estandarización (Z-score)** para normalizar las magnitudes.

### 2.2. Reducción de Dimensionalidad (PCA)
Se aplicó el Análisis de Componentes Principales (PCA) para transformar el espacio de características. 
- Se generó un **Scree-Plot** para evaluar la varianza explicada.
- Se redujo el dataset a las **2 primeras componentes principales**.

### 2.3. Selección de Características
Como enfoque alternativo, se utilizó un modelo de **Random Forest** para calcular la importancia de las variables, seleccionando las 5 características con mayor poder predictivo (ej. Alcohol, Acidez Volátil, Sulfatos).

### 2.4. Agrupamiento (K-Means)
Se ejecutó el algoritmo K-Means en tres escenarios experimentales:
1. Dataset Original Completo.
2. Dataset reducido por PCA (2 componentes).
3. Dataset con selección de características (Top 5).
Se evaluaron valores de **K entre 2 y 6** utilizando el Método del Codo y el Coeficiente de Silueta.

## 3. Resultados y Análisis

### 3.1. Análisis de PCA y Scree-Plot
El Scree-Plot reveló que la primera componente (PC1) explica el **29%** de la varianza y la segunda (PC2) el **17%**. En conjunto, las dos primeras componentes capturan el **46% de la varianza total** del dataset. Esta reducción permite una representación visual efectiva sin perder los patrones estructurales principales.

### 3.2. Comparación de Clustering (K-Means)
A partir de la evaluación de métricas, se observaron los siguientes resultados:

| Versión del Dataset | Silhouette Score Máximo (K=2) | Inercia (K=2) | Observación |
| :--- | :---: | :---: | :--- |
| **PCA (2 Comp)** | **~0.40** | **~3,500** | **Máxima separación y cohesión.** |
| **Selección de Variables** | ~0.22 | ~4,500 | Resultados consistentes pero con solapamiento. |
| **Dataset Original** | ~0.22 | ~10,300 | Alta complejidad y baja separación. |

### 3.3. Interpretación de los Gráficos
- **Método del Codo**: El dataset original presenta una inercia muy elevada debido a la dimensionalidad. En contraste, la versión de PCA muestra una curva mucho más controlada con un punto de inflexión sugerido en **K=2 o K=3**.
- **Coeficiente de Silueta**: PCA es el único enfoque que logra superar el umbral de 0.40, lo que valida que la reducción de dimensionalidad eliminó ruido que dificultaba el agrupamiento en el espacio original.

## 4. Conclusiones
- **PCA como facilitador**: La reducción de dimensionalidad mediante PCA mejora drásticamente la calidad del agrupamiento métrico, logrando casi duplicar el Silhouette Score del dataset original.
- **Configuración óptima**: Se determina que **K=2** es el número óptimo de clústeres para este dataset, representando posiblemente una segmentación base entre perfiles químicos de alta y baja calidad.
- **Eficiencia**: El uso de solo 2 componentes principales (46% de varianza) es suficiente para superar en calidad de agrupamiento al uso de todas las variables originales o a la selección manual de las mismas.

---
**Autor:** Juan Guillermo Marulanda Mesa  
**Fecha:** Mayo 2026  
**Curso:** Ciencia de Datos 2
