
# Detección de Fraude en Tarjetas de Crédito usando SVM

Este proyecto implementa un modelo de clasificación para detectar transacciones fraudulentas utilizando el algoritmo de **Máquinas de Soporte Vectorial (SVM)**.

## Objetivo

El objetivo del proyecto es construir un modelo de Machine Learning que pueda identificar transacciones fraudulentas en un conjunto de datos de transacciones con tarjetas de crédito. El dataset está altamente desbalanceado, con una proporción muy pequeña de fraudes en comparación con las transacciones legítimas.

## Pasos del Proyecto

### 1. Carga y Exploración del Dataset

El conjunto de datos utilizado tiene 284,807 registros y 31 columnas. Las columnas **V1** a **V28** representan características transformadas mediante PCA por motivos de privacidad, mientras que las columnas **Time**, **Amount**, y **Class** son variables importantes.

- **Time**: Indica el tiempo transcurrido desde la primera transacción.
- **Amount**: Monto de la transacción.
- **Class**: La variable objetivo que indica si la transacción fue fraudulenta (1) o legítima (0).

El dataset está altamente desbalanceado con un 99.83% de transacciones legítimas y solo un 0.17% de transacciones fraudulentas.

### 2. Limpieza y Normalización de Características

Dado el alto desbalance en el dataset y la naturaleza de los datos, se realizaron los siguientes pasos de preprocesamiento:

- **Normalización del monto**: Se utilizó el `StandardScaler` para normalizar la columna **Amount**, asegurando que los valores estuvieran en una escala comparable con el resto de las características.
- **Manejo del desbalance de clases**: Se empleó el parámetro `class_weight='balanced'` en el modelo SVM para dar mayor importancia a las transacciones fraudulentas, permitiendo que el modelo no se vea sesgado hacia la clase mayoritaria (transacciones legítimas).

### 3. Entrenamiento del Modelo SVM

Se utilizó un modelo de **Máquinas de Soporte Vectorial (SVM)** con el kernel RBF y un balanceo de clases (`class_weight='balanced'`). Este balance asegura que las transacciones fraudulentas reciban mayor importancia durante el entrenamiento.

### 4. Evaluación del Modelo

El modelo fue evaluado utilizando las métricas de precisión, recall, y F1-score. Estas métricas son adecuadas para datasets desbalanceados, donde el **recall** es especialmente importante, ya que indica cuántas transacciones fraudulentas fueron correctamente identificadas.

#### Reporte de Clasificación

```
              precision    recall  f1-score   support

           0       1.00      0.99      1.00     56863
           1       0.06      0.84      0.11        99

    accuracy                           0.99     56962
   macro avg       0.53      0.92      0.55     56962
weighted avg       1.00      0.99      0.99     56962
```

#### Matriz de Confusión

La matriz de confusión mostró que el modelo logró detectar correctamente 83 transacciones fraudulentas de las 99 en el conjunto de prueba.

```
[[56372   491]
 [   16    83]]
```

### 5. Visualización de Resultados

Se generaron dos tipos de gráficos:

- **Matriz de Confusión**: Para mostrar las predicciones correctas e incorrectas del modelo.
- **Gráfico de Barras de Métricas**: Para visualizar las métricas de **precisión**, **recall**, y **F1-score** tanto para la clase legítima como para la fraudulenta.

### 6. Conclusión

El modelo SVM entrenado logró un **recall** del 84% en la clase fraudulenta, lo cual es un resultado positivo dado el alto desequilibrio de clases. A pesar de que la precisión para la clase fraudulenta fue baja, el alto recall es crítico en este tipo de problemas, ya que es más importante identificar la mayor cantidad posible de fraudes. Sin embargo, un enfoque de mejora futura podría incluir técnicas adicionales como **SMOTE** para sobre-muestrear la clase minoritaria y mejorar aún más el rendimiento.

## Archivos

- **credit_card_fraud_svm_cleaning.ipynb**: Notebook con la implementación completa del modelo y los pasos de limpieza y normalización.
- **creditcard.csv**: El dataset utilizado para este proyecto.
