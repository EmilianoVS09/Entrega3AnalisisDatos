# COVID-19 Business Intelligence — Primera Ola Pandémica (ene–jul 2020)

**ITM · Análisis de Datos 2026-1**  
**Dataset:** [Corona Virus Report — Kaggle (imdevskp)](https://www.kaggle.com/datasets/imdevskp/corona-virus-report)  
**Período analizado:** 22 de enero de 2020 — 27 de julio de 2020  
**Registros:** 49,068 | **Países:** 187 | **Regiones OMS:** 6

---

## Equipo

| Integrante | 
|---|
| Carlos Alberto Moreno David |
| Juan Esteban García Ocampo |
| Emiliano Vélez Suárez |
| Sebastián Ciro Medellín |

---

## Video de presentación

[![Video de presentación](https://img.youtube.com/vi/7SAEXrc7fkY/0.jpg)](https://youtu.be/7SAEXrc7fkY)

---

## Objetivo

Desarrollar un proyecto integral de Business Intelligence sobre los datos de la primera ola de COVID-19, transformando datos epidemiológicos crudos en información útil para la toma de decisiones mediante dashboards, indicadores y análisis estadístico. El proyecto busca responder tres preguntas clave:

1. ¿Existen diferencias significativas en la tasa de letalidad (CFR) entre las regiones de la OMS?
2. ¿Cuáles fueron los períodos de mayor aceleración en la propagación global y qué regiones los lideraron?
3. ¿Qué países presentaron las trayectorias de recuperación más eficientes y qué los distingue del resto?

---

## Metodología

El proyecto se desarrolló en seis fases encadenadas:

### Fase 1 — Comprensión del problema
Análisis exploratorio completo del dataset: estructura, calidad de datos, análisis univariado (distribuciones, outliers, asimetría) y multivariado (correlaciones, scatter plots, evolución temporal). Se identificaron problemas de calidad como el subregistro de recuperados en Reino Unido, valores negativos en casos activos por correcciones retroactivas, y una distribución fuertemente asimétrica en todas las variables numéricas.

### Fase 2 — Formulación de hipótesis
Se plantearon dos hipótesis formales y se validaron estadísticamente:

- **H1:** La CFR difiere significativamente entre regiones de la OMS → validada con **ANOVA de un factor**
- **H2:** Los países con brote más tardío presentan una CFR final más baja → evaluada con **Correlación de Pearson** (unilateral)

### Fase 3 — Preparación y modelado de datos
Limpieza del dataset (recálculo de casos activos, tratamiento de negativos, normalización de campos) y construcción de un **modelo dimensional en esquema estrella** con cuatro tablas: `hechos_covid_diario`, `dim_pais_snapshot`, `dim_region` y `dim_fecha`.

### Fase 4 — Definición de KPIs
Definición, cálculo e interpretación de 7 KPIs con justificación desde el negocio y relación con las hipótesis:

| KPI | Descripción | Valor global |
|---|---|---|
| KPI 1 | Tasa de Letalidad (CFR) | 3.97% |
| KPI 2 | Tasa de Recuperación | 57.45% |
| KPI 3 | Active Rate | 38.58% |
| KPI 4 | Índice de Mortalidad sobre Recuperados (IMR) | 6.94 |
| KPI 5 | Días desde primer caso global (mediana) | 41 días |
| KPI 6 | Media móvil 7 días de nuevos confirmados (MA7) | Pico: 252,437/día |
| KPI 7 | Coeficiente de Gini de casos | 0.82 |

### Fase 5 — Dashboard en Power BI
Construcción de un dashboard interactivo con 4 páginas y modelo estrella conectado:

- **Ejecutivo:** KPIs globales, mapa coroplético y tendencia de MA7
- **Regional (H1):** Validación visual del ANOVA, CFR por región, tabla comparativa
- **Temporal (H2):** Scatter timing vs CFR, oleadas secuenciales por región
- **Países:** Ranking por Recovery Rate, Gini, tabla detallada por país

Filtros globales de fecha y región OMS disponibles en todas las páginas.

### Fase 6 — Análisis, validación y storytelling
Síntesis de todos los resultados, narrativa epidemiológica estructurada en tres actos, propuesta de decisiones basadas en evidencia y discusión de limitaciones metodológicas.

---

## Resultados

### Hipótesis

| Hipótesis | Prueba | Estadístico | p-valor | Decisión |
|---|---|---|---|---|
| H1: La CFR difiere entre regiones OMS | ANOVA un factor | F(5, 148) = 2.3237 | 0.0458 | **Se rechaza H₀** ✓ |
| H2: Correlación negativa timing–CFR | Correlación de Pearson (unilateral) | r = −0.1291 | 0.0552 | No se rechaza H₀ ✗ |

**H1:** Existe evidencia estadísticamente significativa de que la CFR no es igual en todas las regiones de la OMS. Europa presenta la mayor CFR media (4.43%), con una diferencia significativa respecto a África (2.27%), confirmada por t-test post-hoc (t = 3.25, p = 0.0016). La región OMS explica el 7.3% de la varianza en la CFR (η² = 0.073).

**H2:** La correlación negativa esperada entre el timing del brote y la CFR final no alcanzó significancia estadística (r = −0.129, p unilateral = 0.055). La dirección del efecto es la esperada, pero la magnitud es demasiado débil para superar el umbral con la muestra disponible. No es posible confirmar ni refutar la hipótesis con estos datos.

### Hallazgos principales

- **Patrón de oleadas secuenciales:** Asia (ene–feb) → Europa (mar–abr) → Américas (may–jul 2020). Al cierre del dataset, las Américas concentraban más del 50% de los nuevos casos diarios globales con curva aún ascendente.
- **Alta concentración de la carga epidémica:** el coeficiente de Gini de 0.82 indica que aproximadamente el 15% de los países concentra el 80% de los casos confirmados globales.
- **Benchmarks de recuperación:** Alemania, Corea del Sur y China lograron tasas de recuperación superiores al 80%, asociadas a estrategias de trazabilidad temprana y testeo masivo.
- **Subregistro crítico:** Reino Unido no reportó cifras de recuperación de forma sistemática, lo que distorsiona cualquier comparación directa de Recovery Rate que lo incluya.

---

## Conclusiones

**Sobre las hipótesis:**
La pandemia de COVID-19 durante la primera ola no fue un fenómeno homogéneo. La CFR varió significativamente entre regiones del mundo, lo que confirma que factores sistémicos —capacidad diagnóstica, estructura demográfica y preparación hospitalaria— determinaron la gravedad de las consecuencias en cada región. Esta diferencia es estadísticamente real y no puede atribuirse al azar.

La hipótesis sobre la curva de aprendizaje global (H2) no pudo confirmarse estadísticamente con los datos disponibles, aunque la dirección del efecto y el p-valor marginal (0.055) sugieren que la relación podría existir con una muestra mayor o con variables de control adicionales.

**Sobre el proyecto:**
El Business Intelligence aplicado a datos epidemiológicos permite pasar de la descripción al análisis causal y de allí a recomendaciones accionables. Los dashboards construidos demuestran que una CFR global promedio es un indicador engañoso: oculta disparidades regionales estadísticamente demostradas que deberían orientar estrategias diferenciadas de respuesta en salud pública.

**Limitaciones principales:**
- La capacidad de testeo desigual entre países introduce un sesgo sistemático en la CFR que no puede corregirse sin datos adicionales.
- El dataset no incluye variables poblacionales (tasas per cápita) ni indicadores de respuesta institucional (capacidad de UCI, índices de stringencia), que explicarían parte importante de la varianza residual en la CFR (92.7% no explicado por la región OMS).
- El corte temporal en julio de 2020 limita las conclusiones a la primera ola; las oleadas posteriores y el impacto de las vacunas no están reflejados.

---

## Estructura del repositorio

```
ENTREGA 3/
├── Dashboard/
│   ├── pbicovid.pbix
│   └── Presentacion_Interactiva_COVID19.html
├── Data/
│   ├── Processed/
│   │   ├── PowerBI/
│   │   │   ├── dim_fecha.xlsx
│   │   │   ├── dim_pais_snapshot.xlsx
│   │   │   ├── dim_region.xlsx
│   │   │   └── hechos_covid_diario.xlsx
│   │   ├── diccionario_modelo.csv
│   │   ├── dim_fecha.csv
│   │   ├── dim_pais_snapshot.csv
│   │   ├── dim_region.csv
│   │   └── hechos_covid_diario.csv
│   └── covid_19_clean_complete.csv
├── Notebooks/
│   ├── Analisis_validacion_storytelling.ipynb
│   ├── Comprension_Problema.ipynb
│   ├── Definicion_KPIs.ipynb
│   ├── Formulacion_Hipotesis.ipynb
│   └── Preparacion_Modelado.ipynb
├── recursos/
├── .gitignore
└── README.md
```
---

*Proyecto desarrollado para la asignatura Análisis de Datos — ITM 2026-1*