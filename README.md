# Proyecto 2 - Hipótesis: Análisis de la Industria Musical 🎶

## Enlaces y recursos 🔗

- [Dataset en BigQuery](https://docs.google.com/spreadsheets/d/1ExoXrMWxENQ_GJLLsV74gePR1lMM3O8-FlRoyyLusF8/edit?gid=1296584158#gid=1296584158)
- [Dashboard en Power BI](https://drive.google.com/file/d/1Ah9KHYqqxYhmIvuOssBZpm24FPqVwgbt/view?usp=drive_link)
- [Google Colab](https://colab.research.google.com/drive/1-1OjZNxA-QhJuLesfAf0zM5olRXuBwKn?usp=sharing)
- [Presentación en Google Slides](https://docs.google.com/presentation/d/19uHTEeJTFAXgoo6gKVKS8IBQGSNT0EOBI4rilc8q_ic/edit#slide=id.g2770393657e_0_139)
- [Video de presentación en Loom](https://www.loom.com/share/77928d5e64db42369c57cb1d2e946452?sid=f88bd9b5-46ec-4014-b1e6-1a9c08359d42)

## Descripción 📖

Este proyecto aborda el lanzamiento de un nuevo artista en el competitivo escenario musical utilizando un dataset de Spotify con las canciones más escuchadas de 2023. La discográfica planteó una serie de hipótesis sobre los factores que influyen en el éxito de una canción, y este análisis tiene como objetivo validar dichas hipótesis para tomar decisiones estratégicas informadas.

## Planteamiento del Problema

### Hipótesis:

1. Las canciones con un mayor BPM (Beats Por Minuto) tienen más éxito en términos de streams.
2. Las canciones populares en Spotify también son exitosas en otras plataformas como Deezer.
3. Las canciones presentes en más playlists tienden a tener más streams.
4. Los artistas con más canciones tienen más streams.
5. Las características musicales influyen en el número de streams.

## Objetivo 🎯

Validar o refutar las hipótesis propuestas mediante análisis de datos para identificar los factores que más influyen en el éxito musical.

## Equipo 👥

- **Nova Gallardo**
- **Lorna Remmele**

## Herramientas y Tecnologías 🛠️

- **BigQuery**
- **SQL**
- **Python (Google Colab)**
- **Power BI**
- **Google Slides**
- **Loom**

## Estructura del Proyecto 🗂️

### 1. Procesamiento y Preparación de los Datos 📊

- **Conectar los datos**: El dataset de Spotify fue conectado a BigQuery.
- **Manejo de valores nulos y duplicados**: Se eliminaron o imputaron valores faltantes y duplicados.
- **Manejo de datos fuera del alcance**: Se filtraron datos irrelevantes, como canciones de años anteriores.
- **Manejo de outliers y valores discrepantes**: Se gestionaron valores extremos, especialmente en variables numéricas como streams y BPM.
- **Creación de nuevas variables**: Se crearon variables como el número de playlists y la interacción con otras plataformas.
- **Unión de tablas**: Los datos se unieron y consolidaron en un único dataset para facilitar el análisis.

### 2. Análisis Exploratorio 🕵️‍♀️

- **Visualización de categorías**: Gráficos para explorar distribuciones y relaciones entre variables como género musical y popularidad.
- **Medidas de tendencia central y dispersión**: Análisis de la media, mediana y desviación estándar para streams y BPM.
- **Análisis temporal**: Gráficos de línea para observar patrones de popularidad a lo largo del tiempo.
- **Correlación entre variables**: Se calcularon correlaciones entre variables clave para validar las hipótesis.

### 3. Validación de Hipótesis ✔️

1. **Hipótesis 1: Las canciones con mayor BPM tienen más streams**
    - **Resultado**: La prueba de normalidad Shapiro-Wilk indicó que los streams no siguen una distribución normal. A través de la prueba Mann-Whitney U, se concluyó que **no hay una diferencia significativa** entre las canciones de alto y bajo BPM en cuanto a la cantidad de streams obtenidos. Esta hipótesis fue **refutada**.
2. **Hipótesis 2: Las canciones populares en Spotify también lo son en Deezer**
    - **Resultado**: Se confirmó una **correlación moderada** entre la popularidad de las canciones en Spotify y Deezer utilizando scatter plots. Por lo tanto, la popularidad de las canciones en una plataforma es consistente con su popularidad en la otra. Esta hipótesis fue **confirmada**.
3. **Hipótesis 3: Más playlists implican más streams**
    - **Resultado**: La prueba Mann-Whitney U mostró una diferencia altamente significativa (p < 0.05) entre las canciones incluidas en más playlists y aquellas con menos. Cuantas más playlists incluyan una canción, **mayor es el número de streams** que recibe. Esta hipótesis fue **confirmada**.
4. **Hipótesis 4: Los artistas con más canciones tienen más streams**
    - **Resultado**: A través de box plots y scatter plots, se observó una correlación positiva entre el número de canciones de un artista y la cantidad de streams. Artistas con más canciones en Spotify tienden a generar más streams. Esta hipótesis fue **confirmada**.
5. **Hipótesis 5: Las características musicales influyen en los streams**
    - **Resultado**: Las pruebas Mann-Whitney U revelaron que dos características específicas, **danceability** y **speechiness**, tienen un impacto significativo en el número de streams, mientras que otras características no mostraron una relación significativa. Esta hipótesis fue **parcialmente confirmada**.

### 4. Creación del Dashboard 📊

- **Resumen en scorecards**: Se resumen los principales insights en scorecards que muestran métricas clave como la cantidad de playlists y su influencia en los streams.
- **Visualizaciones interactivas en Power BI**: Gráficos que muestran las principales correlaciones y tendencias de popularidad.

## Resultados Clave 🔑

1. **El BPM no es un factor determinante**: Las canciones con un mayor BPM no necesariamente tienen más streams, según el análisis estadístico realizado.
2. **Popularidad en múltiples plataformas**: La correlación entre Spotify y Deezer es clara; las canciones que son populares en una plataforma también lo son en la otra.
3. **Impacto de las playlists**: La cantidad de playlists en las que se incluye una canción tiene un impacto directo y significativo en el número de streams, validando la importancia de la presencia en múltiples listas de reproducción.
4. **Número de canciones por artista**: Los artistas con un mayor catálogo tienden a recibir más streams, lo que sugiere que una estrategia de lanzamiento frecuente podría ser efectiva.
5. **Características clave en la música**: Las canciones con altos valores de **danceability** y **speechiness** tienen más probabilidades de ser exitosas en términos de streams.

## Recomendaciones Estratégicas 📈

1. **Optimizar el lanzamiento en temporadas de baja competitividad**: Se recomienda lanzar nuevas canciones en momentos con menor competitividad por streams, como los meses de verano (junio a septiembre) y evitar los días de lanzamiento común, como el primer día del mes.
2. **Enfocarse en playlists**: Aumentar la presencia de las canciones en playlists es esencial para maximizar la cantidad de streams. Se debe trabajar activamente para incluir nuevas canciones en una variedad de listas de reproducción, tanto oficiales como generadas por usuarios.
3. **Campañas en redes sociales**: Promover las canciones a través de tendencias en redes sociales como TikTok es clave para crear un efecto viral. Ejemplos recientes han mostrado que canciones virales en TikTok han disparado su popularidad en plataformas de streaming.
4. **Foco en el género pop**: Dado que el género pop sigue siendo dominante y las artistas femeninas tienen gran relevancia en esta categoría, se recomienda seguir lanzando música pop y aprovechar el contexto actual del “Recession Pop” para conectarse con las audiencias en tiempos de recesión.
