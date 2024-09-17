# Representar datos a través de tabla resumen o scorecards

- Primero generamos tablas resumen por separado para cada característica técnica y sus segmentos (alta y baja).

```python
# Agrupar por 'streams_category' y calcular medidas de tendencia para 'streams_int'
summary = data.groupby('streams_category')['streams_int'].agg(['count', 'min', 'max', 'mean', 'median', 'std']).reset_index()

# Renombrar las columnas para que sean más legibles
summary.columns = ['streams_category', 'Count', 'Min', 'Max', 'Mean', 'Median', 'Std']

print("\nResumen para streams_category:\n")
print(summary)
```
<img width="593" alt="Screenshot 2024-07-11 at 19 28 10" src="https://github.com/user-attachments/assets/b3aeeb23-f761-4b95-bd22-9c87b3bec532">

```python
# Agrupar por 'bpm_category' y calcular medidas de tendencia para 'bpm'
summary = data.groupby('bpm_category')['bpm'].agg(['count', 'min', 'max', 'mean', 'median', 'std']).reset_index()

# Renombrar las columnas para que sean más legibles
summary.columns = ['bpm_category', 'Count', 'Min', 'Max', 'Mean', 'Median', 'Std']

print("\nResumen para bpm_category:\n")
print(summary)
```
<img width="582" alt="Screenshot 2024-07-11 at 19 29 09" src="https://github.com/user-attachments/assets/6f42acfb-c41e-4c24-a852-788eb00c534b">

```python
# Agrupar por 'playlists_category' y calcular medidas de tendencia para 'total_playlists
summary = data.groupby('playlists_category')['total_playlists'].agg(['count', 'min', 'max', 'mean', 'median', 'std']).reset_index()

# Renombrar las columnas para que sean más legibles
summary.columns = ['playlists_category', 'Count', 'Min', 'Max', 'Mean', 'Median', 'Std']

print("\nResumen para playlists_category:\n")
print(summary)
```
<img width="676" alt="Screenshot 2024-07-11 at 19 29 32" src="https://github.com/user-attachments/assets/ba6d30b0-12b2-45a1-85b8-dc2366838790">

```python
# Agrupar por 'danceability_category' y calcular medidas de tendencia para 'danceability_%'
summary = data.groupby('danceability_category')['danceability_%'].agg(['count', 'min', 'max', 'mean', 'median', 'std']).reset_index()

# Renombrar las columnas para que sean más legibles
summary.columns = ['danceability_category', 'Count', 'Min', 'Max', 'Mean', 'Median', 'Std']

print("\nResumen para danceability_category:\n")
print(summary)
```
<img width="632" alt="Screenshot 2024-07-11 at 19 29 53" src="https://github.com/user-attachments/assets/95cb1e4c-6614-4224-ba5a-836f89a922c7">

```python
# Agrupar por 'valende_category' y calcular medidas de tendencia para 'valence_%'
summary = data.groupby('valence_category')['valence_%'].agg(['count', 'min', 'max', 'mean', 'median', 'std']).reset_index()

# Renombrar las columnas para que sean más legibles
summary.columns = ['valence_category', 'Count', 'Min', 'Max', 'Mean', 'Median', 'Std']

print("\nResumen para valence_category:\n")
print(summary)
```
<img width="592" alt="Screenshot 2024-07-11 at 19 30 15" src="https://github.com/user-attachments/assets/9af1c5c4-9a7a-4136-8aba-c5472d0a2d44">

```python
# Agrupar por 'energy_category' y calcular medidas de tendencia para 'energy_%'
summary = data.groupby('energy_category')['energy_%'].agg(['count', 'min', 'max', 'mean', 'median', 'std']).reset_index()

# Renombrar las columnas para que sean más legibles
summary.columns = ['energy_category', 'Count', 'Min', 'Max', 'Mean', 'Median', 'Std']

print("\nResumen para energy_category:\n")
print(summary)
```
<img width="585" alt="Screenshot 2024-07-11 at 19 30 35" src="https://github.com/user-attachments/assets/ce32b878-fdad-4ef1-b3f7-03f9b759e1b3">

```python
# Agrupar por 'acousticness_category' y calcular medidas de tendencia para 'acousticness_%'
summary = data.groupby('acousticness_category')['acousticness_%'].agg(['count', 'min', 'max', 'mean', 'median', 'std']).reset_index()

# Renombrar las columnas para que sean más legibles
summary.columns = ['acousticness_category', 'Count', 'Min', 'Max', 'Mean', 'Median', 'Std']

print("\nResumen para acousticness_category:\n")
print(summary)
```
<img width="642" alt="Screenshot 2024-07-11 at 19 30 54" src="https://github.com/user-attachments/assets/d4569635-5837-4667-9b76-ecea0242796c">

```python
# Agrupar por 'instrumentalness_category' y calcular medidas de tendencia para 'instrumentalness_%'
summary = data.groupby('instrumentalness_category')['instrumentalness_%'].agg(['count', 'min', 'max', 'mean', 'median', 'std']).reset_index()

# Renombrar las columnas para que sean más legibles
summary.columns = ['instrumentalness_category', 'Count', 'Min', 'Max', 'Mean', 'Median', 'Std']

print("\nResumen para instrumentalness_category:\n")
print(summary)
```
<img width="649" alt="Screenshot 2024-07-11 at 19 31 12" src="https://github.com/user-attachments/assets/7a63292d-306b-4307-ba1b-477eb7ead298">

```python
# Agrupar por 'liveness_category' y calcular medidas de tendencia para 'liveness_%'
summary = data.groupby('liveness_category')['liveness_%'].agg(['count', 'min', 'max', 'mean', 'median', 'std']).reset_index()

# Renombrar las columnas para que sean más legibles
summary.columns = ['liveness_category', 'Count', 'Min', 'Max', 'Mean', 'Median', 'Std']

print("\nResumen para liveness_category:\n")
print(summary)
```
<img width="603" alt="Screenshot 2024-07-11 at 19 31 30" src="https://github.com/user-attachments/assets/04afffaa-ed1d-407d-a31f-e0d481656434">

```python
# Agrupar por 'speechiness_category' y calcular medidas de tendencia para 'speechiness_%'
summary = data.groupby('speechiness_category')['speechiness_%'].agg(['count', 'min', 'max', 'mean', 'median', 'std']).reset_index()

# Renombrar las columnas para que sean más legibles
summary.columns = ['speechiness_category', 'Count', 'Min', 'Max', 'Mean', 'Median', 'Std']

print("\nResumen para speechiness_category:\n")
print(summary)
```
<img width="615" alt="Screenshot 2024-07-11 at 19 31 50" src="https://github.com/user-attachments/assets/9a5105d5-8e2e-4fbd-adf0-d28d1f8b92e1">

### Tabla resumen con las medidas de tendencia para todas las categorías continuas

```python
features_medidas_tendencias = [
    'streams_int',
    'total_playlists',
    'bpm',
    'danceability_%',
    'valence_%',
    'energy_%',
    'acousticness_%',
    'instrumentalness_%',
    'liveness_%',
    'speechiness_%'
]

# Crear una tabla resumen con las medidas de tendencia para todas las categorías continuas
summary = data[features_medidas_tendencias].agg(['count', 'min', 'max', 'mean', 'median', 'std']).transpose()
summary.rename(columns={'count': 'Count', 'mean': 'AVG', 'median': 'MEDIAN', 'std': 'SD'}, inplace=True)

print("\nResumen:\n")
print(summary)
```
<img width="666" alt="Screenshot 2024-07-11 at 19 33 56" src="https://github.com/user-attachments/assets/646053b4-42f5-4d03-9cce-1c75b631e819">

<img width="290" alt="Screenshot 2024-07-11 at 19 34 34" src="https://github.com/user-attachments/assets/1ac6a08b-29eb-4cef-bef0-40e4a55f8574">

