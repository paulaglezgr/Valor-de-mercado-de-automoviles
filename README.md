# 🚗 Predicción del Valor de Mercado de Autos Usados

## 📝 Descripción General

Este proyecto se enfoca en la creación de un modelo de Machine Learning para Regresión capaz de predecir con precisión el valor de mercado de vehículos usados. El servicio de venta de autos Rusty Bargain necesita esta solución para una nueva aplicación que permitirá a los clientes estimar rápidamente el precio de su coche basándose en especificaciones técnicas, versión de equipamiento e historial.

El desafío principal es encontrar un equilibrio óptimo entre calidad de predicción (RMSE), velocidad de predicción y tiempo de entrenamiento del modelo.

## 🎯 Objetivos del Proyecto

El cliente, Rusty Bargain, requiere que el modelo optimice tres métricas clave:
* Calidad de Predicción: Minimizar el error (evaluado con RMSE).
* Velocidad de Predicción: El modelo debe ser rápido al estimar el precio.
* Tiempo de Entrenamiento: El proceso de entrenamiento debe ser eficiente en tiempo.

## ⚙️ Metodología
### 1. Preprocesamiento y Limpieza de Datos
Se realizó una limpieza exhaustiva del conjunto de datos para garantizar la integridad y la calidad de las variables de entrenamiento:

* Valores Ausentes y Duplicados: Se eliminaron 262 filas duplicadas. Los valores ausentes en características categóricas (como vehicle_type, gearbox, model, fuel_type) se rellenaron con el marcador 'unknown'.
* Transformación de Variables: La columna not_repaired (sin reparar) se codificó de forma binaria, transformando 'yes' a 1 y 'no' a 0, y tratando los NaNs como 0.
* Manejo de Outliers: Se filtraron valores irrealistas en las columnas clave:
  * price: Se estableció un rango razonable, eliminando precios de $0 y tomando un mínimo de $800.
  * registration_year: Se acotó el rango de años de registro a valores lógicos (ej. 1950 < año < 2024).
  * power: Se restringió la potencia (CV) a un rango físicamente coherente (ej. 75 - 500 CV).


### 2. Modelado y Entrenamiento
Se evaluaron múltiples algoritmos de regresión, incluyendo modelos lineales y modelos de aumento de gradiente, para comparar su rendimiento en las tres métricas de interés. Las características categóricas se codificaron utilizando One-Hot Encoding (OHE) para los modelos tradicionales.

Modelos evaluados:

* Regresión Lineal (LR)

* Árbol de Decisión (AD)

* Bosque Aleatorio (RF)

* Gradient Boosting: LightGBM (LGBMR), CatBoost (CBR), y XGBoost (XGBR)

## El análisis de rendimiento concluyó que:

* **Modelo Principal** Seleccionado: LightGBM se posicionó como el modelo más equilibrado y eficiente. Ofreció una excelente calidad de predicción (bajo RMSE) con un tiempo de entrenamiento y predicción rápido.

* **Modelo Alternativo**: CatBoost también demostró ser una alternativa robusta y bien balanceada, obteniendo un puntaje muy cercano al LightGBM.

La solución final propuesta para Rusty Bargain es implementar el modelo LightGBM como el motor de predicción principal, utilizando el modelo CatBoost como respaldo en caso de necesidad de estabilidad crítica.
