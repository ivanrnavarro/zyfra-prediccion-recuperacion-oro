# Predicción de la recuperación de oro — Zyfra

Proyecto integrado del bootcamp de Ciencia de Datos de TripleTen, aplicado a un proceso industrial de extracción y purificación de oro.

## Problema de negocio

Zyfra desarrolla soluciones de eficiencia para la industria minera. El objetivo es construir un modelo que prediga la **recuperación de oro** en dos etapas del proceso, la flotación (*rougher*) y la purificación final, para optimizar la producción y descartar parámetros de operación poco rentables.

## Datos

Datos de proceso con mediciones por etapa (alimentación, flotación, purificación primaria y secundaria):

- Conjunto de entrenamiento: 16.860 registros y 87 variables.
- Conjunto de prueba: 5.856 registros y 53 variables.
- Conjunto completo: 22.716 registros y 87 variables.

El conjunto de prueba no incluye las variables de salida ni los cálculos de cada etapa, lo que simula el escenario real de operación y obliga a entrenar solo con variables disponibles al momento de predecir.

## Metodología

1. **Validación del cálculo de recuperación**: se recalculó la recuperación de la etapa *rougher* a partir de las concentraciones y se comparó con el valor registrado (error absoluto medio del orden de 10⁻¹⁵).
2. **Análisis de las variables ausentes** en el conjunto de prueba para evitar fuga de información.
3. **Preprocesamiento**: tratamiento de valores faltantes y filtrado de registros anómalos.
4. **Análisis del proceso**:
   - Evolución de la concentración de oro, plata y plomo en cada etapa.
   - Concentraciones en las colas, como indicador de pérdidas.
   - Comparación de la distribución del tamaño de partícula entre entrenamiento y prueba.
   - Detección de concentraciones totales anómalas.
5. **Métrica de evaluación**: implementación propia de **sMAPE** y del sMAPE final, que combina las dos etapas.
6. **Modelado** con validación cruzada: regresión lineal y bosque aleatorio para cada etapa.
7. **Evaluación en el conjunto de prueba**.

## Resultados

- **sMAPE final de 9,73 %** en el conjunto de prueba, coherente con lo obtenido en validación cruzada.
- **Etapa *rougher***: la regresión lineal logra el menor error, con bajo costo computacional.
- **Etapa final**: el bosque aleatorio describe mejor la recuperación.

## Hallazgos del proceso

- La concentración de oro aumenta más de 5 veces desde la alimentación hasta la purificación final, lo que indica un proceso de extracción eficiente.
- La plata se concentra en la flotación, pero su concentración cae en las etapas de purificación y se acumula en las colas. Esto sugiere evaluar el reprocesamiento de ese efluente.

## Próximos pasos

- Probar modelos adicionales con mejor desempeño y bajo costo computacional.
- Hacer un análisis de sensibilidad de los hiperparámetros del bosque aleatorio.

## Herramientas

Python · pandas · NumPy · Matplotlib · seaborn · scikit-learn

## Archivos

- [`zyfra_prediccion_recuperacion_oro.ipynb`](zyfra_prediccion_recuperacion_oro.ipynb): notebook completo con código, gráficos y análisis.
- `requirements.txt`: librerías utilizadas.

Los datos fueron proporcionados por TripleTen y no se incluyen en el repositorio. El notebook conserva las salidas de la ejecución original.

---

**Iván Ricardo Navarro Espinosa** — Ingeniero Químico, MSc · [GitHub](https://github.com/ivanrnavarro) · ivanrnavarro@gmail.com
Más proyectos del bootcamp en [tripleten-ciencia-de-datos](https://github.com/ivanrnavarro/tripleten-ciencia-de-datos).
