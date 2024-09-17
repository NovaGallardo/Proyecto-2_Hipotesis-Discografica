# Unir tablas

<aside>
💡 Generar previamente una limpieza de las tablas importadas.

</aside>

## track_in_spotify_clean

```sql
SELECT
track_id,
LOWER (REGEXP_REPLACE(track_name, r'[^a-zA-Z0-9]', ' ')) AS track_name_clean,
LOWER (REGEXP_REPLACE(artists_name, r'[^a-zA-Z0-9]', ' ')) AS artists_name_clean,
artist_count, released_day, released_month, released_year,
CAST(CONCAT(released_year, '-', released_month, '-', released_day) AS DATE) AS released_date,
CASE
  WHEN (released_month = 3 AND released_day >= 20) OR (released_month IN (4, 5)) OR (released_month = 6 AND released_day < 20) THEN 'spring'
  WHEN (released_month = 6 AND released_day >= 20) OR (released_month IN (7, 8)) OR (released_month = 9 AND released_day < 22) THEN 'summer'
  WHEN (released_month = 9 AND released_day >= 22) OR (released_month IN (10, 11)) OR (released_month = 12 AND released_day < 21) THEN 'fall'
  WHEN (released_month = 12 AND released_day >= 21) OR (released_month IN (1, 2)) OR (released_month = 3 AND released_day < 20) THEN 'winter'
END AS season,
in_spotify_playlists, in_spotify_charts,
SAFE_CAST(streams AS INT64) AS streams_int,
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_spotify`
WHERE
track_id NOT IN (CAST(5675634 AS STRING), CAST(4586215 AS STRING), CAST(4967469 AS STRING))
#eliminar track_id de canciones repetidas
```

<aside>
💡 Crear vista para “track_in_spotify” bajo el nombre “track_in_spotify_clean”. Con CASE + WHEN(AND) OR(IN) se creó una columna para obtener la temporada en que la canción fue publicada. También se dejaron las columnas de día, mes y año y se creó una columna nueva con la fecha completa con CAST(CONCAT) AS DATE.

</aside>

## track_in_competition_clean

```sql
CREATE OR REPLACE `laboratoria-426816.proyecto2_hipotesis.track_in_competition_clean`
SELECT *,
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_competition`
WHERE
 in_shazam_charts IS NOT NULL
 OR in_deezer_charts IS NOT NULL
 OR in_deezer_playlists IS NOT NULL
 OR in_apple_charts IS NOT NULL
 OR in_apple_playlists IS NOT NULL
 OR track_id IS NOT NULL
```

## track_technical_info_clean

```sql
CREATE OR REPLACE `laboratoria-426816.proyecto2_hipotesis.track_technical_info_clean`
SELECT *
FROM `laboratoria-426816.proyecto2_hipotesis.track_technical_info`
WHERE
key IS NOT NULL
```

## **Unir las tres tablas con LEFT JOIN**

<aside>
💡 Como la tabla final contiene 2 columnas duplicadas adicionales (track_id_1 y track_id_2), usamos SELECT para excluirlas de antemano. La vista con la unión de tablas se llama **“track_all_data”.**

</aside>

```sql
SELECT
CASE
  WHEN s.track_id = '0:00' THEN '000'
  ELSE s.track_id
END AS track_id,
s.track_name_clean,
s.artists_name_clean,
s.artist_count,
CASE
  WHEN artist_count = 1 THEN 'solo'
  WHEN artist_count > 1 THEN 'feat'
  ELSE NULL
END AS artist_category,
s.released_day,
s.released_month,
s.released_year,
s.released_date,
s.season,
s.in_spotify_playlists,
s.in_spotify_charts,
s.streams_int,
c.in_shazam_charts,
c.in_deezer_charts,
c.in_deezer_playlists,
c.in_apple_charts,
c.in_apple_playlists,
s.in_spotify_playlists +  c.in_deezer_playlists +  c.in_apple_playlists AS total_playlists,
t.key,
t.bpm,
t.mode,
t.`danceability_%`,
t.`valence_%`,
t.`energy_%`,
t.`acousticness_%`,
t.`instrumentalness_%`,
t.`liveness_%`,
t.`speechiness_%`,
q.streams_category,
q.playlists_category,
q.popularity,
q.bpm_category,
q.danceability_category,
q.valence_category,
q.energy_category,
q.acousticness_category,
q.instrumentalness_category,
q.liveness_category,
q.speechiness_category
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_spotify_clean` AS S
LEFT JOIN
`laboratoria-426816.proyecto2_hipotesis.track_in_competition_clean` AS C
ON
S.track_id = C.track_id
LEFT JOIN
`laboratoria-426816.proyecto2_hipotesis.track_technical_info_clean` AS T
ON
S.track_id = T.track_id
LEFT JOIN
`laboratoria-426816.proyecto2_hipotesis.quartiles` AS q
ON
S.track_id = q.track_id

```

<aside>
💡 “S.in_spotify_playlists + C.in_deezer_playlists + C.in_apple_playlists AS total_playlists” es para crear una nueva columna con la suma de todas las playlists. 

Con CASE + ELSE + END AS cambiamos a “000” el track_id que era “0:00”. También se creó la columna “artist_category_ para saber si el artista es solista o es una colaboración.

s.in_spotify_playlists +  c.in_deezer_playlists +  c.in_apple_playlists AS total_playlists, se sumó el total de playlist de cada canción.

</aside>

## **Crear track_all_data en una misma consulta**

```sql
WITH track_in_spotify_clean_2 AS (
SELECT
track_id,
LOWER (REGEXP_REPLACE(track_name, r'[^a-zA-Z0-9]', ' ')) AS track_name_clean,
LOWER (REGEXP_REPLACE(artists_name, r'[^a-zA-Z0-9]', ' ')) AS artists_name_clean,
artist_count, released_day, released_month, released_year,
CAST(CONCAT(released_year, '-', released_month, '-', released_day) AS DATE) AS released_date,
CASE
  WHEN (released_month = 3 AND released_day >= 20) OR (released_month IN (4, 5)) OR (released_month = 6 AND released_day < 20) THEN 'spring'
  WHEN (released_month = 6 AND released_day >= 20) OR (released_month IN (7, 8)) OR (released_month = 9 AND released_day < 22) THEN 'summer'
  WHEN (released_month = 9 AND released_day >= 22) OR (released_month IN (10, 11)) OR (released_month = 12 AND released_day < 21) THEN 'fall'
  WHEN (released_month = 12 AND released_day >= 21) OR (released_month IN (1, 2)) OR (released_month = 3 AND released_day < 20) THEN 'winter'
END AS season,
in_spotify_playlists, in_spotify_charts,
SAFE_CAST(streams AS INT64) AS streams_int,
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_spotify`
WHERE
track_id NOT IN (CAST(5675634 AS STRING), CAST(4586215 AS STRING), CAST(4967469 AS STRING))
),
track_in_competition_clean_2 AS (
SELECT *,
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_competition`
WHERE
in_shazam_charts IS NOT NULL
OR in_deezer_charts IS NOT NULL
OR in_deezer_playlists IS NOT NULL
OR in_apple_charts IS NOT NULL
OR in_apple_playlists IS NOT NULL
OR track_id IS NOT NULL
),
track_technical_info_clean_2 AS (
SELECT *
FROM `laboratoria-426816.proyecto2_hipotesis.track_technical_info`
WHERE
key IS NOT NULL
)
SELECT
s.track_id,
s.track_name_clean,
s.artists_name_clean,
s.artist_count,
CASE
   WHEN artist_count = 1 THEN 'solo'
   WHEN artist_count > 1 THEN 'feat'
   ELSE NULL
 END AS artist_category,
s.released_day,
s.released_month,
s.released_year,
s.released_date,
s.season,
s.in_spotify_playlists,
s.in_spotify_charts,
s.streams_int,
c.in_shazam_charts,
c.in_deezer_charts,
c.in_deezer_playlists,
c.in_apple_charts,
c.in_apple_playlists,
s.in_spotify_playlists +  c.in_deezer_playlists +  c.in_apple_playlists AS total_playlists,
t.key,
t.bpm,
t.mode,
t.`danceability_%`,
t.`valence_%`,
t.`energy_%`,
t.`acousticness_%`,
t.`instrumentalness_%`,
t.`liveness_%`,
t.`speechiness_%`,
FROM
`laboratoria-426816.proyecto2_hipotesis.track_in_spotify_clean` AS s
LEFT JOIN
`laboratoria-426816.proyecto2_hipotesis.track_in_competition_clean` AS c
ON
s.track_id = c.track_id
LEFT JOIN
`laboratoria-426816.proyecto2_hipotesis.track_technical_info_clean` AS t
ON
s.track_id = t.track_id
```
