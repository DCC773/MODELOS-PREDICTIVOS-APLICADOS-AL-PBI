# 📊 Predicción del PBI Real Anual de Perú

## 1. Introducción
Este proyecto tiene como objetivo principal **comparar distintos modelos de series de tiempo y aprendizaje automático** para predecir y explicar el crecimiento del **Producto Bruto Interno (PBI) real anual del Perú**.

La economía peruana ha atravesado periodos de crecimiento sostenido, así como etapas de desaceleración asociadas a factores políticos, choques externos y, de manera particular, al impacto de la pandemia de **COVID-19**. Analizar y comprender la dinámica del PBI resulta fundamental para una evaluación económica adecuada y para la toma de decisiones de política económica.

En este estudio se evalúan los siguientes modelos:

- Red Neuronal Artificial (RNA)  
- ARIMA  
- ARIMAX (incorporando una variable dummy para el impacto del COVID-19)  
- Filtro de Kalman  

Cada modelo es evaluado utilizando métricas como el **Error Cuadrático Medio (MSE)** y el **Coeficiente de Determinación (R²)**, además de comparaciones gráficas que permiten identificar cuál se ajusta mejor a los datos históricos.

---

## 2. Descripción de los Datos

### 📌 Variables
**Variable dependiente**
- Crecimiento del PBI real anual (%)

**Variables independientes / exógenas**
- Tasa de inflación  
- Consumo (% del PBI)  
- Inversión (% del PBI)  
- Gasto público (% del PBI)  
- Exportaciones netas (XN)

### 📊 Fuentes de datos
- Banco Central de Reserva del Perú (BCRP)  
- Banco Mundial  
- Ministerio de Economía y Finanzas (MEF)

---

## 3. Modelos Aplicados

### 3.1 Red Neuronal Artificial (RNA)

#### 🧠 Arquitectura del modelo
- Capa de entrada: 5 neuronas  
  *(Inflación, Gasto Público, Consumo Privado, Inversión y Exportaciones Netas)*  
- Capa oculta: 10 neuronas (ReLU)  
- Capa de salida: 1 neurona (activación lineal)

#### ⚙️ Configuración
- Optimizador: Adam  
- Función de pérdida: MSE  
- Regularización: EarlyStopping

#### 📈 Resultados
- **MSE**: 7.38  
- **RMSE**: 2.72  
- **R²**: 0.3911  
- **Proyección PBI 2025**: **1.74 %**

> El modelo captura adecuadamente la tendencia general del PBI, aunque presenta limitaciones frente a eventos extremos, como la caída económica de 2020.

---

### 3.2 Modelo ARIMA

- Modelo univariado basado únicamente en la serie histórica del PBI.
- Diferenciación de primer orden para lograr estacionariedad.
- Selección de órdenes mediante el criterio AIC.

#### 📈 Resultados ARIMA(0,1,2)
- **MSE**: 18.0349  
- **R²**: 0.0550  
- **Proyección PBI 2025**: **2.59 %**

> El modelo presenta una capacidad explicativa limitada, aunque los residuos no muestran autocorrelación, lo que valida su consistencia estadística.

---

### 3.3 Modelo ARIMAX

- Extensión del ARIMA con una variable dummy para capturar el impacto del COVID-19 en 2020.

#### 📈 Resultados ARIMAX(0,1,2)
- **MSE**: 9.9352  
- **R²**: 0.4603  
- **Proyección PBI 2025**: **4.72 %**  
- **Intervalo de confianza (95%)**: `[-1.31 %, 10.75 %]`

> La inclusión de la variable exógena mejora significativamente el ajuste y el poder explicativo del modelo.

---

### 3.4 Filtro de Kalman

- Modelo de espacio de estados para estimar el crecimiento subyacente del PBI, filtrando el ruido de la serie.

#### 📈 Resultados
- **MSE**: 11.2651  
- **R²**: 0.3880  
- **Proyección PBI 2025**: **2.49 %**

> El Filtro de Kalman permite estimar de forma eficiente el estado “real” del PBI y su evolución dinámica en el tiempo.

---

## 4. Conclusiones Generales

### 🔎 Comparación de errores
- **ARIMAX** presenta el menor error y el mejor ajuste global.
- **Red Neuronal** y **Filtro de Kalman** muestran un desempeño aceptable.
- **ARIMA** es el modelo con menor capacidad predictiva.

### 📊 Poder explicativo (R²)
- **ARIMAX**: 46% de la variación explicada.
- **RNA y Kalman**: aproximadamente 39%.
- **ARIMA**: poder explicativo muy bajo.

### 📅 Proyecciones para 2025
- ARIMAX: **4.72 %**
- Filtro de Kalman: **2.49 %**
- ARIMA: **2.59 %**
- Red Neuronal: **1.74 %**

📌 **Referencia BCRP**: 3.10 %

### ✅ Recomendación final
El **modelo ARIMAX(0,1,2) con dummy de COVID-19** es el enfoque más robusto para predecir el crecimiento del PBI real anual del Perú, al combinar precisión, poder explicativo y capacidad para incorporar choques externos.

---
