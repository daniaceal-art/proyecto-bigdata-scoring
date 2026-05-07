# proyecto-bigdata-scoring

Equipo de trabajo:
Daniela Acevedo Álvarez-
Juan Rafael Taborda

# 1.	CASO DE NEGOCIO
   
Descripción del Problema: Las entidades financieras presentan dificultades en la recuperación de cartera debido a la ausencia de capacidades analíticas avanzadas que permitan anticipar el riesgo de incumplimiento de los clientes. Actualmente, la gestión de cobranza se apoya en reglas estáticas y análisis descriptivo, lo que limita la capacidad de priorizar esfuerzos, incrementa la mora, reduce la tasa de recuperación y genera pérdidas económicas.
La disponibilidad de grandes volúmenes de datos transaccionales, demográficos, comportamentales y de pagos no está siendo aprovechada de forma integral para predecir el comportamiento de pago y optimizar las estrategias de cobranza

1.1 Objetivo general
Diseñar e implementar una solución de Big Data en Databricks que permita analizar grandes volúmenes de información de clientes y predecir el riesgo de no pago, con el fin de optimizar los procesos de recuperación de cartera y mejorar los indicadores de morosidad.

1.2 Objetivos específicos:

•	Construir un modelo analítico que permita clasificar a los clientes según su nivel de riesgo de incumplimiento (bajo, medio, alto).scorin de cobranza si requerimos un modelo por l

•	Integrar y procesar datos estructurados y no estructurados (histórico de pagos, transacciones, comportamiento de consumo, variables sociodemográficas).

•	Optimizar las estrategias de cobranza, priorizando clientes de alto riesgo con acciones diferenciadas.

Esta solución permitirá pasar de un enfoque reactivo a uno predictivo en la gestión de cartera.

# 2.	Análisis económico
La implementación de un modelo de scoring predictivo de cobranza genera beneficios económicos directos en la gestión de cartera y permite una gestión anticipada del riesgo.

Reducción de costos operativos

Antes del modelo:

•	Evaluaciones manuales de riesgo 

•	Análisis reactivo de mora 

•	Procesos repetitivos de seguimiento

Con el Databricks:

•	El análisis de riesgo se automatiza mediante Machine Learning

•	Se reducen tiempos de análisis y carga operativa del equipo

Esto implica una disminución significativa de costos operativos y mayor eficiencia en la gestión de clientes.

Así mismo el modelo  permite identificar clientes con alta probabilidad de incumplimiento antes de que entren en mora.

Gracias a esto se pueden aplicar estrategias preventivas:

•	Seguimiento temprano a clientes de alto riesgo lo cual reduce la cartera castigada y mejorar tasas de recuperación

•	Priorización de acciones de cobranza

La solución propuesta no solo optimiza el análisis de datos, sino que genera impacto financiero positivo al reducir pérdidas por incumplimiento y mejorar la eficiencia operativa.

# 3.Arquitectura Propuesta:

Excel → Databricks Volume → Tabla Bronze → Tabla Silver→ Modelo Machine Learning → Tabla Gold → Databricks Job  → Dashboard Power BI

Fuente de Datos:

La base contiene información histórica de clientes con variables demográficas, financieras y de comportamiento de pago.

Almacenamiento (Volumes):

El archivo se carga en Databricks Volumes, que actúa como capa de almacenamiento en la nube.

Bronze – Datos crudos:

Se realiza la carga del archivo en una tabla con el objetivo de conservar la información original sin ningún tipo de transformación.

Silver – Transformación:

Se aplican procesos de calidad y preparación de los datos, como:

• Limpieza de los nombres de las columnas

• Conversión de los tipos de datos

• Estandarización de las variables

Los datos quedan listos para análisis y modelado.

Machine Learning – Scoring de riesgo:

Se entrena un modelo de regresión logística para estimar la probabilidad de que cada cliente incumpla sus obligaciones.

Resultado generado:

score_riesgo

Gold-Datos para negocio:

Se crea la tabla final:

gold_scoring_clientes

Contiene:

•	Variables del cliente 

•	Probabilidad de incumplimiento 

•	Score de riesgo 

Esta tabla está lista para consumo analítico.

Jobs:

Automatización del pipeline

Power Bi:

La tabla Gold se conecta a Power BI para crear dashboards interactivos.

El dashboard permite:

•	Monitorear riesgo de cartera 

•	Identificar clientes de alto riesgo 

•	Analizar indicadores clave

La arquitectura combina Big Data, Machine Learning y Business Intelligence en un flujo completo que permite analizar la información de principio a fin

# 4 Pipeline De Ingesta De Datos:
La información se obtiene desde un archivo Excel almacenado en Databricks Volumes y es procesada mediante notebooks que ejecutan cada una de las etapas del flujo de datos.

Automatización de la ingesta:
La carga de datos se realiza utilizando notebooks en Databricks, los cuales permiten leer, procesar y almacenar grandes volúmenes de información en tablas Delta Lake.
Este proceso puede integrarse con Databricks Workflows, permitiendo programar ejecuciones automáticas y garantizando la actualización periódica de la información sin intervención manual.

Estrategia Medallion:

Se implementa una arquitectura en capas que organiza los datos según su nivel de procesamiento:

Bronze-Datos crudos:

Se realiza la carga inicial del archivo Excel sin aplicar transformaciones.

Tabla generada: bronze_clientes

Silver-Transformación y enriquecimiento:

Se aplican procesos de limpieza y preparación de los datos, tales como:

• Renombramiento de columnas

• Conversión de tipos de datos

• Eliminación de valores o caracteres inválidos

• Estandarización de la información

Tabla generada: silver_clientes
Propósito:

• Garantizar calidad, consistencia y usabilidad de los datos

Gold-Datos para negocio:

Se consolidan los datos y se integran con el modelo de Machine Learning para generar el scoring de riesgo.
Propósito:

• Disponer de información lista para análisis

• Apoyar la toma de decisiones mediante indicadores y score de riesgo

Pipelines  y Workflows:

El pipeline completo se automatiza mediante Databricks Workflows la ejecución de la arquitectura de datos, permitiendo procesar la información de forma continua desde su origen hasta la generación de valor para el negocio.

# 5 MODELOS DE CIENCIA DE DATOS:

Análisis descriptivo

Se realizó exploración estadística de variables financieras y demográficas de los clientes, identificando variables clave relacionadas con el incumplimiento:

•	Días en mora 

•	Cuotas en mora 

•	Uso del cupo 

•	Nivel de ingresos

Se implementó un modelo de Regresión Logística para predecir la probabilidad de incumplimiento.
El dataset fue dividido:

•	80% entrenamiento 

•	20% prueba 

Resultado obtenido:
Accuracy del modelo: 93.4%
El modelo permite calcular la probabilidad de incumplimiento para cada cliente, generando un score de riesgo.

# Lineage:

Se utilizó la funcionalidad Lineage Graph de Databricks Unity Catalog para validar la trazabilidad de los datos.

Notebook de ingestión y transformación (Pipeline_bigdata) 

Tabla Bronze → bronze_clientes 

Tabla Silver → silver_clientes 

Tabla Gold → gold_scoring_clientes 

El linaje garantiza gobernanza, auditoría y control del ciclo de vida del dato dentro de la arquitectura.

# 6 APP O VISUALIZACIÓN:
Visualización:


Se desarrolló un dashboard en Power BI para visualizar los resultados generados por el modelo.

El dashboard permite:

•	Analizar el score de riesgo de los clientes 

•	Identificar segmentos con mayor probabilidad de incumplimiento 

La visualización se alimenta de la tabla gold_scoring_clientes, que contiene la información consolidada y lista para análisis

Adicional el modelo queda desplegado como un servicio de analítica que permite generar predicciones de forma periódica y disponibilizarlas para consumo por herramientas de negocio.

