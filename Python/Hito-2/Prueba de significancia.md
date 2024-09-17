# Prueba de significancia

Definición de las **hipótesis**:

- **h0:** No existen diferencias significativas entre los promedios de streams de cada segmento (alto, bajo) de característica técnica (danceability, acousticness, valence, etc).
- **h1:** Sí existen diferencias significativas entre los promedios de streams de cada segmento (alto, bajo) de característica técnica (danceability, acousticness, valence, etc).

Elegir un nivel de confianza y por tanto el **Alpha**. Nivel de confianza de la prueba: 95%, es decir, si repitiéramos 100 veces la prueba, en 5 veces la conclusión no sería la misma que estamos aceptando. El Alpha sería 1 - 0,95 = 0,05. Es decir, 0,05 sería el término de contraste.

En el código la diferencia en ejecutar el test t y ejecutar el test de Wilcoxon (Mann-Whitney U) es que para el test t ejecutamos la función **stats.ttest_ind** y para el Wilcoxon ejecutamos la función **stats.mannwhitneyu**. 

**Realizar test Shapiro-Wilk** para determinar si la distribución de datos es normal o no y en base a eso decidir si aplicamos test t o test de Wilcoxon. El código aplica automáticamente el test adecuado y arroja el resultado.

```python
# Importación de librerías necesarias
from google.colab import files
import pandas as pd
from scipy.stats import ttest_ind, mannwhitneyu, shapiro
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

# Cargar datos
load=files.upload()

# Asegurarse de que los datos se han cargado correctamente
data=pd.read_excel(load["track_all_data.xlsx"])

#Visualización de la data cargada
data.head()

# Lista de características a probar
features_categories = [
    'bpm_category_test',
    'playlists_category',
    'danceability_category',
    'valence_category',
    'energy_category',
    'acousticness_category',
    'instrumentalness_category',
    'liveness_category',
    'speechiness_category'
]

# Función para realizar la prueba de Shapiro-Wilk y determinar si se debe usar prueba t o prueba de Mann-Whitney U
def normality_test_and_statistical_test(data, category_col):
    # Filtrar filas con valores nulos en las columnas de categorías
    filtered_data = data.dropna(subset=[category_col, 'streams_int'])

    # Filtrar los grupos de alto y bajo según la categoría
    high_group = filtered_data[filtered_data[category_col] == 'alta']['streams_int']
    low_group = filtered_data[filtered_data[category_col] == 'baja']['streams_int']

    # Prueba de Shapiro-Wilk para determinar la normalidad
    shapiro_high = shapiro(high_group)
    shapiro_low = shapiro(low_group)

    print(f'Shapiro-Wilk Test for {category_col} - High streams: p-value = {shapiro_high.pvalue}')
    print(f'Shapiro-Wilk Test for {category_col} - Low streams: p-value = {shapiro_low.pvalue}')

    # Decidir qué prueba estadística usar
    if shapiro_high.pvalue > 0.05 and shapiro_low.pvalue > 0.05:
        # Ambos grupos siguen una distribución normal, usamos la prueba t
        t_stat, t_pvalue = ttest_ind(high_group, low_group)
        print(f'T-Test for {category_col}: t-statistic = {t_stat}, p-value = {t_pvalue}')
    else:
        # Al menos uno de los grupos no sigue una distribución normal, usamos la prueba de Mann-Whitney U
        u_stat, u_pvalue = mannwhitneyu(high_group, low_group)
        print(f'Mann-Whitney U Test for {category_col}: U-statistic = {u_stat}, p-value = {u_pvalue}')

    print('\n')

# Realizar las pruebas para cada característica
for category in features_categories:
    normality_test_and_statistical_test(data, category)

```

<aside>
❕ **Resultados**

Shapiro-Wilk Test for bpm_category_test - High streams: p-value = 3.8795251790908144e-26
Shapiro-Wilk Test for bpm_category_test - Low streams: p-value = 4.794922886405495e-25
Mann-Whitney U Test for bpm_category_test: U-statistic = 104345.0, p-value = 0.06539277164202092

Shapiro-Wilk Test for playlists_category - High streams: p-value = 7.903930989782272e-19
Shapiro-Wilk Test for playlists_category - Low streams: p-value = 1.6670170438680325e-25
Mann-Whitney U Test for playlists_category: U-statistic = 208266.0, p-value = 1.4696980893855468e-115

Shapiro-Wilk Test for danceability_category - High streams: p-value = 3.992961220220058e-27
Shapiro-Wilk Test for danceability_category - Low streams: p-value = 3.468798499530011e-24
Mann-Whitney U Test for danceability_category: U-statistic = 103017.5, p-value = 0.030910607295619102

Shapiro-Wilk Test for valence_category - High streams: p-value = 1.3633211260570145e-26
Shapiro-Wilk Test for valence_category - Low streams: p-value = 1.093277595380369e-24
Mann-Whitney U Test for valence_category: U-statistic = 106411.0, p-value = 0.17663342962989492

Shapiro-Wilk Test for energy_category - High streams: p-value = 9.199461683606202e-26
Shapiro-Wilk Test for energy_category - Low streams: p-value = 1.117665279569083e-25
Mann-Whitney U Test for energy_category: U-statistic = 107072.0, p-value = 0.2324269060567119

Shapiro-Wilk Test for acousticness_category - High streams: p-value = 6.27831167750274e-27
Shapiro-Wilk Test for acousticness_category - Low streams: p-value = 2.7301044147156242e-24
Mann-Whitney U Test for acousticness_category: U-statistic = 104422.5, p-value = 0.06809494525575559

Shapiro-Wilk Test for instrumentalness_category - High streams: p-value = 7.934415986305006e-26
Shapiro-Wilk Test for instrumentalness_category - Low streams: p-value = 1.8114020088316014e-25
Mann-Whitney U Test for instrumentalness_category: U-statistic = 106065.5, p-value = 0.15164311738331276

Shapiro-Wilk Test for liveness_category - High streams: p-value = 1.4525614350424973e-24
Shapiro-Wilk Test for liveness_category - Low streams: p-value = 2.1491547775542406e-26
Mann-Whitney U Test for liveness_category: U-statistic = 107950.5, p-value = 0.3244343052223113

Shapiro-Wilk Test for speechiness_category - High streams: p-value = 2.0451378820040115e-27
Shapiro-Wilk Test for speechiness_category - Low streams: p-value = 5.868957896332421e-24
Mann-Whitney U Test for speechiness_category: U-statistic = 100922.5, p-value = 0.007912261694498395

</aside>

<aside>
💡

- **Danceability_category**:
    - Hay una diferencia significativa en la cantidad de streams entre canciones con alta y baja `danceability`.
    - Esto sugiere que `danceability` puede influir en el número de streams, pero no especifica si esta influencia es positiva o negativa.
- **Speechiness_category**:
    - Hay una diferencia significativa en la cantidad de streams entre canciones con alta y baja `speechiness`.
    - Similarmente, esto sugiere que `speechiness` puede influir en el número de streams.
- **Playlists_category**:
    - Hay una diferencia altamente significativa en la cantidad de streams entre canciones con alta y baja presencia en playlists.
    - Esto sugiere que estar presente en más playlists tiene un impacto significativo en el número de streams.
</aside>

### Función para crear gráficos de distribución para entender la distribución de los datos

```python
# Función para crear gráficos de distribución
def plot_distribution(data, category, feature):
    sns.boxplot(x=category, y=feature, data=data)
    plt.title(f'Distribución de {feature} por {category}')
    plt.show()

# Visualizar distribuciones para categorías significativas
plot_distribution(data, 'danceability_category', 'streams_int')
plot_distribution(data, 'speechiness_category', 'streams_int')
plot_distribution(data, 'playlists_category', 'streams_int')
```
![Untitled](https://github.com/user-attachments/assets/535d2818-f804-4b0d-b310-2d958d653c3c)

![Untitled2](https://github.com/user-attachments/assets/533702d7-6d87-4e3c-9903-b39747cda838)

![Untitled3](https://github.com/user-attachments/assets/e9360161-d28a-47d8-874b-4cdcebc7f1cf)
