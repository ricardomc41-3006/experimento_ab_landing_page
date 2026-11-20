# 🧪 Evaluación de Experimento A/B en Landing Page (E-commerce)

## 🎯 Objetivo del Proyecto
Evaluar estadísticamente un experimento A/B realizado en una página de inicio (*landing page*) con dos variantes (**A** y **B**) sobre una muestra de 40,000 usuarios, con el fin de respaldar con datos una decisión de negocio enfocada en maximizar la **tasa de conversión** y el **ticket promedio**.

## 📁 Conjunto de Datos Utilizado
El análisis se basa en el dataset `landing_experiment.csv` (40,000 registros únicos y 9 columnas, sin valores nulos, correspondiente al periodo del 1 al 28 de enero de 2026), con un balanceo de tráfico 50/50 entre la variante A (19,982 usuarios) y la variante B (20,018 usuarios):

* **Identificación y tiempo:** `user_id`, `date`.
* **Segmentación:** `landing` (A/B), `region`, `dispositivo`, `traffic_source`, `user_type`.
* **Métricas de negocio:** `converted` (binaria) y `gasto` (numérica).

## 🛠️ Etapas del Análisis Realizadas
1. **Validación de Calidad e Integridad del Experimento (EDA):** Verificación de usuarios duplicados, contaminación de muestra (usuarios expuestos a ambas variantes), balanceo 50/50, tipificación de fechas (`datetime`) y consistencia lógica entre conversión y gasto.
2. **Comparación de Gasto Promedio (A vs. B):** Validación de supuestos de normalidad (**Shapiro-Wilk**) y homocedasticidad (**Levene**), aplicación de la **prueba t de Welch** (`equal_var=False`) y respaldo no paramétrico con **U de Mann-Whitney**.
3. **Comparación de Tasa de Conversión (A vs. B):** Aplicación de la **prueba Z para proporciones** (*Z-test*) con `statsmodels`.
4. **Segmentación Categórica:** Pruebas **Chi-cuadrada de independencia** para evaluar la asociación entre `traffic_source` y `user_type` frente a la conversión.
5. **Visualización y Traducción a Negocio:** Gráficos comparativos de volumen absoluto y barras apiladas al 100% (proporción relativa) en Matplotlib/Seaborn, cerrando con un Insight Ejecutivo accionable.

## 💡 Hallazgos Clave
* **Superioridad en Ticket Promedio:** La variante **B** generó un gasto promedio de **$68.75** frente a **$61.09** de la variante A ($p = 0.00000$ en Welch y Mann-Whitney U), incentivando compras de mayor volumen.
* **Superioridad en Conversión:** La variante **B** alcanzó una tasa de conversión de **15.96%**, superando ampliamente el **12.57%** de la variante A ($p = 0.00000$ en Z-test).
* **Dependencia por Fuente de Tráfico:** Existe asociación estadísticamente significativa ($p = 0.03414$). **Email (14.99%)** y **Ads (14.74%)** lideran la eficiencia de conversión, mientras que **Organic (13.79%)** aporta el mayor volumen absoluto de visitantes.
* **Independencia por Tipo de Usuario:** No existe diferencia significativa ($p = 0.47363$) entre usuarios **Nuevos (14.36%)** y **Recurrentes (14.09%)**, confirmando que la experiencia funciona de forma transversal.

## 📌 Recomendaciones de Negocio
1. **Desplegar la variante B al 100% del tráfico inmediatamente:** Domina tanto en volumen de conversiones como en ticket promedio.
2. **Estandarizar sin segmentar por historial de usuario:** No es necesario invertir recursos en versiones separadas para usuarios nuevos y recurrentes.
3. **Capitalizar el tráfico orgánico con *retargeting*:** Implementar campañas de **Ads** y **Email** dirigidas a usuarios orgánicos que visitaron la página B sin concretar compra.

## 🚀 Cómo ejecutar el Notebook (Guía de Reproducción)
**Requisitos previos:**
* Python 3.8 o superior.
* Librerías: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `statsmodels`.

**Ejecución:**
1. Clona este repositorio: git clone https://github.com/ricardomc41-3006/experimento_ab_landing_page.git
