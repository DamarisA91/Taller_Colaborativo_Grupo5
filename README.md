# Taller_Colaborativo_Grupo5
# UNIVERSIDAD DE ESPECIALIDADES ESPIRITU SANTO

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

**Base de datos:** *Product Classification and Clustering*

Link: https://archive.ics.uci.edu/dataset/837/product%2Bclassification%2Band%2Bclustering

**Descripción:**
Este conjunto de datos se recopiló de PriceRunner, una popular plataforma de comparación de productos. Incluye 35 311 ofertas de productos de 10 categorías, proporcionadas por 306 comerciantes diferentes. 

**Variables de entrada:**

<div align="center">
    <img src="https://github.com/user-attachments/assets/e3e7fdd1-f434-4160-bdb2-880b598da787" width="100%" />
</div>

## METODOLOGÍA:
**PREPROCESAMIENTO DE LOS DATOS:**
Se utilizó los campos numéricos para que la visualización con sns.pairplot, sean óptimas. Cada fila representa una oferta de un producto por parte de un comerciante. Se codificó todas las variables categóricas y se realizó el escalado de los datos.


**MODELOS:**
### 1.	Clustering con K-Means: 

<div align="center">
    <img src="https://github.com/user-attachments/assets/5ec6c386-631e-417d-aad4-769898a547e2"/>
</div>

<br>

<div align="center">
    <img src="https://github.com/user-attachments/assets/d4757e12-c374-4118-b5ce-c9cab2122a36"/>
</div>

### 2.	Clustering con DBSCAN: 

<div align="center">
    <img src="https://github.com/user-attachments/assets/62a4b530-deff-4503-bb57-72098d216f1d"/>
</div>

<br>

<div align="center">
    <img src="https://github.com/user-attachments/assets/d1a260af-9790-4b12-8cdb-7b8b93e9572f"/>
</div>

### 3.	Reducción de dimensionalidad con PCA:

<div align="center">
    <img src="https://github.com/user-attachments/assets/9d2de615-c3d3-4420-b302-2b1dac2993c2"/>
</div>

<br>

<div align="center">
    <img src="https://github.com/user-attachments/assets/f7d1f00c-b12c-4420-9c0c-7ccce07db38f"/>
</div>

Interpretación detallada de Reducción de dimensionalidad con PCA:

<div align="center">
    <img src="https://github.com/user-attachments/assets/e8c137b2-ca99-42af-8e50-9ef7295497e7" />
</div>

Interpretación del Cluster 0, después de haber reducido los datos con PCA, para facilitar la visualización y mejorar el rendimiento.

Todos los productos pertenecen a la misma categoría (Category ID 2617) y mismo Cluster ID real (38848), pero provienen de diferentes comerciantes (Merchant ID) y productos distintos.

El modelo los agrupó juntos (Cluster 0), posiblemente porque comparten muchas características similares tras la reducción dimensional con PCA.

### 4.	Reducción de dimensionalidad con t-SNE:
El gráfico t-SNE es una herramienta visual de validación para ver si el clustering con K-Means tiene sentido geométrico en un espacio de menor dimensión. Si ves separación clara por colores, es una señal fuerte de que los clusters reflejan estructuras reales en los datos. Se Observa: Tres grupos compactos de colores bien definidos (café, verde y azul), cada uno separado visualmente, significa que los clusters formados tienen sentido, y los productos dentro de cada grupo tienen patrones similares y que K = 3 fue una buena elección.

<div align="center">
    <img src="https://github.com/user-attachments/assets/db6ea56d-e84a-43ed-9f5a-ee7e4cbffc27"/>
</div>

<br>

<div align="center">
    <img src="https://github.com/user-attachments/assets/cdca8fc7-46b8-4c07-bdc8-a0b5b32ee2a6"/>
</div>

**Cluster 0:** Productos de categoría 2620, con Product ID alto. Pertenecen a un Cluster ID elevado, y son ofrecidos por comerciantes medianos. Interpretación: Podrían ser productos populares o de consumo masivo, en comercios conocidos, pero no grandes.

**Cluster 1:** También en categoría 2620, pero con Merchant ID más alto (comercio más relevante). Cluster ID alto → gran variedad. Interpretación: Productos similares a Cluster 0, pero en comercios más grandes o con más alcance.

**Cluster 2:** Category ID diferente (2613), Product ID bajo, y menor presencia de comercio. Interpretación: Productos distintos, probablemente más antiguos o de nicho, vendidos por comercios más pequeños.

- KMeans_Cluster 0 y 1 coinciden completamente con DBSCAN_Cluster 2. Es decir, todos los puntos que K-Means agrupó en los clusters 0 y 1, DBSCAN los agrupó en el mismo cluster (2). Esto sugiere que DBSCAN ve estos dos grupos como parte de un mismo conjunto denso o núcleo de datos.

- KMeans_Cluster 2 fue dividido por DBSCAN en dos grupos: 4,081 puntos en DBSCAN_Cluster 0 7,426 puntos en DBSCAN_Cluster 1

- Esto indica que KMeans metió todo ese grupo en un solo "saco", pero DBSCAN identificó dos subgrupos estructuralmente diferentes, lo que es una señal de que DBSCAN detecta mejor la forma y densidad de los datos, especialmente en clusters no esféricos o con diferente densidad.

## Reflexión y comunicación:

**1) Qué tipo de perfiles se pueden identificar?**
- Cluster 0: Este grupo agrupa productos con un Product ID muy alto (en miles), indicando productos más recientes o más complejos en el catálogo. Están principalmente dentro de la categoría con ID 2620, que podría representar una subcategoría muy específica de móviles o electrónica.
- Cluster 1: Contiene productos con Product ID intermedio y Merchant ID más alto, lo que puede sugerir productos vendidos por comerciantes más especializados. También predomina la categoría 2620, aunque con distinta dispersión en Cluster ID.
- Cluster 2: Compuesto por productos con Product ID bajo (1 a 100) y Category ID = 2612, este grupo parece representar los productos más antiguos o genéricos, como versiones iniciales de un modelo o productos base en electrónica móvil.

**2) Qué diferencias clave surgieron entre los modelos?**
- K-Means creó 3 clusters claramente segmentados basados en magnitudes numéricas, agrupando productos similares según características cuantitativas (ID, categoría).
- DBSCAN, al no depender de la cantidad de clusters, identificó agrupamientos más densos y logró encontrar patrones de ruido y puntos aislados que K-Means no pudo detectar.
En el cruce de resultados, por ejemplo:
<div align="center">
<img width="248" alt="image" src="https://github.com/user-attachments/assets/aa936fe5-800e-4c6a-9579-7a6c0bd722f3" />
</div>
Muestra cómo DBSCAN detectó subgrupos dentro de un mismo cluster de KMeans (Cluster 2), lo que sugiere que KMeans fue más general y DBSCAN más detallado.


**3) Qué limitaciones encontraron y cómo las abordarían?**
- Limitación de features categóricos: Muchos campos como Product Title, Cluster Label y Category Label no se usaron directamente porque no estaban numerizados. Esto limita el análisis semántico.
*Solución: Aplicar técnicas de codificación como One-Hot Encoding o embeddings de texto para incluir esta información en modelos futuros.*
- Escala y distribución de datos: Algunas variables tienen escalas muy diferentes, lo que puede distorsionar los resultados del clustering.
*Solución: Normalizar todas las variables con StandardScaler antes del clustering.*
- Selección de número de clusters: Elegir k=3 en KMeans fue arbitrario. Aunque se basó en la curva del codo, pueden existir agrupaciones más finas.
*Solución: Utilizar métricas como el índice de silueta o validación cruzada no supervisada para una mejor elección.*
-  DBSCAN depende de parámetros eps y min_samples: Una mala configuración puede producir agrupamientos incorrectos o excesivo "ruido".
*Solución: Ajustar parámetros con Grid Search no supervisado o visualizar los k-dist plots.*
-  Dimensionalidad visual limitada: Aunque t-SNE es excelente para visualizar relaciones locales, puede distorsionar la distancia global entre clusters.
*Solución: Complementar con UMAP o mantener análisis en espacios PCA para mayor interpretación.*
