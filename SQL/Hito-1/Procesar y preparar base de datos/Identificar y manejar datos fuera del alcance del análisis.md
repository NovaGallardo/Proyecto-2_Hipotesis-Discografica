# Identificar y manejar datos fuera del alcance del análisis

## Análisis en track_in_competition

```sql
SELECT  *
EXCEPT (in_apple_charts, in_deezer_charts, in_shazam_charts)
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_competition`
```

<aside>
💡 Dejamos fuera las charts de las distintas plataformas, ya que la mayoría contenían 0 y valores muy bajos en relación a las playlists. Consulta guardada como “track_in_competition_except”.

</aside>

## Análisis en track_technical_info

```sql
SELECT *
FROM laboratoria-426816.proyecto2_hipotesis.track_technical_info
WHERE key IS NOT NULL
```

<aside>
💡  ****Dejamos fuera las filas que contienen null en la columna “key”. Consulta guardada como “track_technical_info_except”.

</aside>

## Análisis en track_in_spotify

```sql
SELECT *
EXCEPT (in_spotify_charts)
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_spotify`
```

<aside>
💡 Eliminamos la columna “in_spotify_charts” que la información sobre charts tanto en ésta como en la la tabla “track_in_competition” contiene mayoritariamente valores 0 o muy bajos. Consulta guardada como “track_in_spotify_except”.

</aside>
