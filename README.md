# PROYECTO INTEGRADOR DE INTELIGENCIA ARTIFICIAL 1
## DESARROLLO DE UN MODELO DE MACHINE LEARNING PARA CLASIFICACIÓN DE FLORES INFECTADAS

INTEGRANTES: ELIZABETH GUERRON, JEAN LUC MORALES, MATHIAS VERA

Este repositorio contiene el desarrollo e implementación de un **pipeline predictivo secuencial en cascada** (Clasificación + Regresión) diseñado en ingeniería para optimizar la toma de decisiones en la aplicación de agroquímicos contra patógenos fúngicos en los invernaderos de Tabacundo, Ecuador. El sistema reemplaza los esquemas rígidos de fumigación calendarizada por un enfoque inteligente basado en datos microclimáticos.

---

## 📁 Estructura del Repositorio

*   **`generacion_dataset.ipynb`**: Notebook de Jupyter que contiene el script de Python para la simulación, limpieza, validación de ingeniería y exportación del conjunto de datos, omitiendo variables de ruido instrumental.
*   **`dataset_flores.csv`**: Matriz de datos con 1,000 registros históricos que consolidan los predictores microclimáticos analizados (`Temperatura_C`, `Humedad_Relativa_Porc`, `Radiacion_Solar_W_m2`) y los objetivos biológicos.
*   **`pipeline_orange.ows`**: Archivo de espacio de trabajo de Orange Data Mining que contiene el flujo visual completo en cascada (Normalización, Clasificación, Filtrado dinámico por fila e Intercambio de Target para Regresión).

---

## ⚙️ Arquitectura del Sistema (Pipeline en Cascada)

El modelo opera bajo la lógica de un **embudo o interruptor inteligente** estructurado en dos fases operacionales consecutivas dentro de Orange:

1.  **Fase 1 (Clasificación):** Determina si el entorno microclimático actual representa un peligro inminente de germinación de esporas (`Presencia_Hongo` = 0 o 1).
2.  **Filtro Intermedio (`Select Rows`):** Si la IA predice un entorno seguro, el flujo se detiene para evitar gastos innecesarios. Si predice infección (1), el registro se envía a la Fase 2.
3.  **Fase 2 (Regresión):** Modifica dinámicamente el objetivo hacia la variable continua `Porcentaje_Plantas_Afectadas`, estimando numéricamente la severidad del daño para calcular la dosis exacta de fungicida.

---

## 📈 Resultados Destacados

El experimento analítico mediante Validación Cruzada de 10 pliegues (*10-fold Cross-Validation*) arrojó métricas que validan por completo las hipótesis planteadas:

*   **Detección de Riesgo (Fase 1):** El algoritmo **Random Forest** demostró un desempeño óptimo con una Exactitud de Clasificación del **99.7%** ($CA = 0.997$) y un Área Bajo la Curva de **1.000** ($AUC$). Modelos como **SVM** demostraron un perfil preventivo conservador ideal para la reducción de falsos negativos.
*   **Estimación de Severidad (Fase 2):** La **Regresión Lineal Múltiple** obtuvo un ajuste del **97.4%** ($R^2 = 0.974$) y un Error Absoluto Medio (**MAE**) de apenas **3.291%**. El sistema es capaz de predecir la tasa de afectación con una desviación marginal de $\pm3.29\%$.

**Impacto Agronómico:** La automatización del flujo restringe las intervenciones químicas exclusivamente a los vectores climáticos de riesgo auténtico, logrando suprimir más de la mitad de las aplicaciones tradicionales calendarizadas en el grupo de control.

---

## Para Utilizarlo

Se debe tener instalado orange data mining para poder abrir el archivo .ows (Orange Workflow) y ver el flujo y los resultados obtenidos.

