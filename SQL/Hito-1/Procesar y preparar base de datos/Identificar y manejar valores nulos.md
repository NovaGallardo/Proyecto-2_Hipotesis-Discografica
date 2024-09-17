## Consultar valores nulos en “track_in_competition”

```sql
SELECT *
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_competition`
WHERE in_shazam_charts IS NULL
  OR in_deezer_charts IS NULL
  OR in_deezer_playlists IS NULL
  OR in_apple_charts IS NULL
  OR in_apple_playlists IS NULL
  OR track_id IS NULL
```

<aside>
💡

**Se detectaron 50 valores nulos en ”in_shazam_charts”** que quizás podrían deberse a que las canciones no se encuentran en la plataforma Shazam.

Guardar consulta como “track_in_competition_nulls” con “Guardar la consulta (versión clásica)”.

Descargar consulta en .csv y Hoja de Cálculos.

</aside>

## Consultar valores nulos en “track_technical_info”

```sql
SELECT *
FROM `laboratoria-426816.proyecto2_hipotesis.track_technical_info`
WHERE track_id IS NULL
  OR bpm IS NULL
  OR key IS NULL
  OR mode IS NULL
  OR `danceability_%` IS NULL
  OR `valence_%` IS NULL
  OR `energy_%` IS NULL
  OR `acousticness_%` IS NULL
  OR `instrumentalness_%` IS NULL
  OR `liveness_%` IS NULL
  OR `speechiness_%` IS NULL
```

<aside>
💡 **Se detectaron 95 valores nulos en “key”.** Es información faltante, ya que las canciones en cuestión sí cuentan con especificación de si la tonalidad es mayor o menor en “mode”.

Guardar consulta como “track_technical_info” con “Guardar la consulta (versión clásica)”.

Descargar consulta en .csv y Hoja de Cálculos.

</aside>

## Consultar valores nulos en “track_in_spotify”

```sql
SELECT *
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_spotify`
WHERE track_id IS NULL
  OR track_name IS NULL
  OR artists_name IS NULL
  OR artist_count IS NULL
  OR released_year IS NULL
  OR released_month IS NULL
  OR released_day IS NULL
  OR in_spotify_playlists IS NULL
  OR in_spotify_charts IS NULL
  OR streams IS NUL
```

<aside>
💡 **“track_in_spotify” no tiene valores nulos.**

Guardar consulta como “track_in_spotify” con “Guardar la consulta (versión clásica)”.

Descargar consulta en .csv y Hoja de Cálculos.

</aside>
