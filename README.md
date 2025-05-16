# Taller_Colaborativo_Grupo5
# UNIVERDIDAD DE ESPECIALIDADES ESPIRITU SANTO

## Aprendizaje No Supervisado

**MATERIA:** APRENDIZAJE AUTOMÁTICO

**PROFESOR**: ING. GLADYS MARÍA VILLEGAS RUGEL

**INTEGRANTES:**
- BYRON PIEDRA
- CHRISTIAN GARCÍA
- IVAN CHÉRREZ
- DAMARIS ALARCÓN

## RESUMEN DEL PROBLEMA: 
**Objetivo:**
Implementar y analizar modelos de aprendizaje no supervisado (K-means, DBSCAN, PCA y t-SNE) para segmentar perfiles de usuario o cliente en un entorno tecnológico. Visualizar resultados, comparar métodos y comunicar conclusiones de forma técnica y visual.

**Base de datos: Product Classification and Clustering**

Link: https://archive.ics.uci.edu/dataset/837/product%2Bclassification%2Band%2Bclustering

Descripción: 
Este conjunto de datos se recopiló de PriceRunner, una popular plataforma de comparación de productos. Incluye 35 311 ofertas de productos de 10 categorías, proporcionadas por 306 comerciantes diferentes. 

**Variables de entrada:**

<img width="429" alt="image" src="https://github.com/user-attachments/assets/e3e7fdd1-f434-4160-bdb2-880b598da787" />

## METODOLOGÍA:
**PREPROCESAMIENTO DE LOS DATOS:**
Se utilizó los campos numéricos para que la visualización con sns.pairplot, sean óptimas. Cada fila representa una oferta de un producto por parte de un comerciante. Se codificó todas las variables categóricas y se realizó el escalado de los datos.


**MODELOS:**
### 1.	Clustering con K-Means: 

<img width="277" alt="image" src="https://github.com/user-attachments/assets/5ec6c386-631e-417d-aad4-769898a547e2" />


<img width="270" alt="image" src="https://github.com/user-attachments/assets/d4757e12-c374-4118-b5ce-c9cab2122a36" />

El Cluster 2, tiene valores promedio de Product ID y Cluster ID mucho más bajos. Podría representar productos de otra categoría o segmento completamente diferente.
El Cluster 1 tiene un valor alto en Merchant ID, lo cual puede indicar que está compuesto por productos vendidos por ciertos comerciantes grandes o específicos.
Las diferencias en Category ID y Cluster ID también reflejan cómo se agrupan productos similares.

### 2.	Clustering con DBSCAN: 

<img width="277" alt="image" src="https://github.com/user-attachments/assets/62a4b530-deff-4503-bb57-72098d216f1d" />


<img width="267" alt="image" src="https://github.com/user-attachments/assets/d1a260af-9790-4b12-8cdb-7b8b93e9572f" />


### 3.	Reducción de dimensionalidad con PCA:

<img width="275" alt="image" src="https://github.com/user-attachments/assets/9d2de615-c3d3-4420-b302-2b1dac2993c2" />


<img width="276" alt="image" src="https://github.com/user-attachments/assets/f7d1f00c-b12c-4420-9c0c-7ccce07db38f" />

Interpretación detallada de Reducción de dimensionalidad con PCA:

<img width="226" alt="image" src="https://github.com/user-attachments/assets/e8c137b2-ca99-42af-8e50-9ef7295497e7" />
Interpretación del Cluster 0, después de haber reducido los datos con PCA, para facilitar la visualización y mejorar el rendimiento.

Todos los productos pertenecen a la misma categoría (Category ID 2617) y mismo Cluster ID real (38848), pero provienen de diferentes comerciantes (Merchant ID) y productos distintos.

El modelo los agrupó juntos (Cluster 0), posiblemente porque comparten muchas características similares tras la reducción dimensional con PCA.

### 4.	Reducción de dimensionalidad con t-SNE:
El gráfico t-SNE es una herramienta visual de validación para ver si el clustering con K-Means tiene sentido geométrico en un espacio de menor dimensión. Si ves separación clara por colores, es una señal fuerte de que los clusters reflejan estructuras reales en los datos. Se Observa: Tres grupos compactos de colores bien definidos (café, verde y azul), cada uno separado visualmente, significa que los clusters formados tienen sentido, y los productos dentro de cada grupo tienen patrones similares y que K = 3 fue una buena elección.

<img width="278" alt="image" src="https://github.com/user-attachments/assets/db6ea56d-e84a-43ed-9f5a-ee7e4cbffc27" />

<img width="270" alt="image" src="https://github.com/user-attachments/assets/cdca8fc7-46b8-4c07-bdc8-a0b5b32ee2a6" />

**Cluster 0:** Productos de categoría 2620, con Product ID alto. Pertenecen a un Cluster ID elevado, y son ofrecidos por comerciantes medianos. Interpretación: Podrían ser productos populares o de consumo masivo, en comercios conocidos, pero no grandes.

**Cluster 1:** También en categoría 2620, pero con Merchant ID más alto (comercio más relevante). Cluster ID alto → gran variedad. Interpretación: Productos similares a Cluster 0, pero en comercios más grandes o con más alcance.

**Cluster 2:** Category ID diferente (2613), Product ID bajo, y menor presencia de comercio. Interpretación: Productos distintos, probablemente más antiguos o de nicho, vendidos por comercios más pequeños

## Análisis Final:

- KMeans_Cluster 0 y 1 coinciden completamente con DBSCAN_Cluster 2. Es decir, todos los puntos que K-Means agrupó en los clusters 0 y 1, DBSCAN los agrupó en el mismo cluster (2). Esto sugiere que DBSCAN ve estos dos grupos como parte de un mismo conjunto denso o núcleo de datos.

- KMeans_Cluster 2 fue dividido por DBSCAN en dos grupos: 4,081 puntos en DBSCAN_Cluster 0 7,426 puntos en DBSCAN_Cluster 1

- Esto indica que KMeans metió todo ese grupo en un solo "saco", pero DBSCAN identificó dos subgrupos estructuralmente diferentes, lo que es una señal de que DBSCAN detecta mejor la forma y densidad de los datos, especialmente en clusters no esféricos o con diferente densidad.
