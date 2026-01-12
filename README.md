📊 Predicción del PBI Real Anual de Perú
1. Introducción

Este proyecto tiene como objetivo principal comparar distintos modelos de series de tiempo y aprendizaje automático para predecir y explicar el crecimiento del Producto Bruto Interno (PBI) real anual del Perú.

La economía peruana ha atravesado periodos de crecimiento sostenido, así como etapas de desaceleración asociadas a factores políticos, choques externos y, de manera particular, al impacto de la pandemia de COVID-19. Analizar y comprender la dinámica del PBI resulta fundamental para una evaluación económica adecuada y para la toma de decisiones de política económica.

En este estudio se evalúan los siguientes modelos:

Red Neuronal Artificial (RNA)

ARIMA

ARIMAX (incorporando una variable dummy para el impacto del COVID-19)

Filtro de Kalman

Cada modelo es evaluado utilizando métricas como el Error Cuadrático Medio (MSE) y el Coeficiente de Determinación (R²), además de comparaciones gráficas que permiten identificar cuál se ajusta mejor a los datos históricos.

2. Descripción de los Datos

Las variables utilizadas en el análisis son las siguientes:

Variable dependiente:

Crecimiento del PBI real anual (%)

Variables independientes / exógenas:

Tasa de inflación

Consumo (% del PBI)

Inversión (% del PBI)

Gasto público (% del PBI)

Exportaciones netas (XN)

Fuentes de datos:

Banco Central de Reserva del Perú (BCRP)

Banco Mundial

Ministerio de Economía y Finanzas (MEF)

3. Modelos Aplicados
3.1 Red Neuronal Artificial (RNA)

Se empleó una red neuronal artificial con la siguiente arquitectura:

Capa de entrada: 5 neuronas (Inflación, Gasto Público, Consumo Privado, Inversión y Exportaciones Netas)

Capa oculta: 10 neuronas con función de activación ReLU

Capa de salida: 1 neurona con activación lineal

El modelo fue compilado utilizando el optimizador Adam y la función de pérdida Mean Squared Error (MSE). Para evitar el sobreajuste, se implementó EarlyStopping, restaurando los mejores pesos obtenidos durante el entrenamiento.

Resultados del modelo RNA:

MSE (datos de prueba): 7.38

RMSE: 2.72

R²: 0.3911

Proyección del PBI para 2025: 1.74 %

La evolución de la función de pérdida muestra que el modelo no presenta sobreajuste, lo que sugiere una adecuada capacidad de generalización. El modelo logra capturar la tendencia general del PBI, aunque presenta limitaciones para reproducir eventos extremos, como la fuerte caída observada en 2020.

3.2 Modelo ARIMA

El modelo ARIMA se estimó utilizando únicamente la serie histórica del crecimiento del PBI. Para garantizar la estacionariedad, se aplicó una diferenciación de primer orden. La selección de los parámetros (p, d, q) se realizó mediante el criterio de información de Akaike (AIC).

Resultados del modelo ARIMA(0,1,2):

MSE: 18.0349

R²: 0.0550

Proyección del PBI para 2025: 2.59 %

El modelo presenta un error moderado y un coeficiente de determinación bajo, lo que indica una capacidad limitada para explicar la variabilidad del PBI. No obstante, el análisis de residuos confirma la ausencia de autocorrelación, validando su consistencia estadística para fines comparativos.

3.3 Modelo ARIMAX

El modelo ARIMAX extiende el enfoque ARIMA al incorporar una variable exógena dummy que captura el impacto del COVID-19 en el año 2020.

Resultados del modelo ARIMAX(0,1,2):

MSE: 9.9352

R²: 0.4603

Proyección del PBI para 2025: 4.72 %

Intervalo de confianza al 95%: [-1.31 %, 10.75 %]

La inclusión de la variable dummy mejora significativamente el ajuste del modelo y su capacidad explicativa, evidenciando la importancia de considerar choques externos en el análisis macroeconómico.

3.4 Filtro de Kalman

El Filtro de Kalman se utilizó para estimar el valor subyacente del crecimiento del PBI, filtrando el ruido presente en la serie y permitiendo realizar proyecciones dinámicas.

Resultados del Filtro de Kalman:

MSE: 11.2651

R²: 0.3880

Proyección del PBI para 2025: 2.49 %

El Filtro de Kalman resulta eficaz para estimar el estado “real” de la serie temporal. Las matrices de transición y observación, estimadas automáticamente mediante el algoritmo kf.em de pykalman, reflejan la dinámica inherente del PBI. Aunque la ganancia de Kalman no se muestra explícitamente, esta desempeña un rol clave en el proceso de actualización del estado, combinando la predicción previa con la nueva información observada.

4. Conclusiones Generales
Comparación de errores (MSE y RMSE)

ARIMAX presenta el menor error, lo que indica el mejor ajuste a los datos históricos y una mayor precisión en las predicciones. Su capacidad para incorporar eventos exógenos, como el COVID-19, resulta determinante.

La Red Neuronal y el Filtro de Kalman muestran errores moderados, reflejando un desempeño aceptable, aunque con dificultades frente a eventos atípicos.

El ARIMA presenta el mayor error, evidenciando que un enfoque puramente autorregresivo es insuficiente para capturar la dinámica del PBI.

Poder explicativo (R²)

El modelo ARIMAX destaca nuevamente, explicando aproximadamente el 46% de la variación del PBI.

La Red Neuronal y el Filtro de Kalman presentan valores similares de R² (alrededor de 0.39), lo que indica una capacidad explicativa razonable.

El ARIMA registra un R² muy bajo, confirmando su limitada capacidad explicativa.

Proyecciones para 2025

Las proyecciones para el año 2025 difieren entre modelos:

ARIMAX: 4.72 %

Filtro de Kalman: 2.49 %

ARIMA: 2.59 %

Red Neuronal: 1.74 %

Como referencia, el BCRP proyecta un crecimiento de 3.10 %.

Recomendación final

Considerando las métricas de error y el poder explicativo, el modelo ARIMAX(0,1,2) con dummy de COVID-19 se posiciona como el enfoque más robusto para predecir el crecimiento del PBI real anual del Perú. Su capacidad para incorporar variables exógenas lo hace superior al ARIMA puro y más preciso que la Red Neuronal y el Filtro de Kalman en este contexto específico.
