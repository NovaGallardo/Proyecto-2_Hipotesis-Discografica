# Calcular cuartiles, deciles o percentiles

## **total_streams y total_playlist**

<aside>
❕ Código para crear una view de quartiles con nuevas variables quartile_streams, quartile_total_playlist, quartile_bpm, popularity y speedness

</aside>

```sql
WITH Quartiles AS (
 SELECT
   s.track_id,
   s.streams_int,
   (s.in_spotify_playlists + c.in_deezer_playlists + c.in_apple_playlists) AS total_playlists,
   t.bpm,
   NTILE(4) OVER (ORDER BY s.streams_int) AS quartile_streams,
   NTILE(4) OVER (ORDER BY (s.in_spotify_playlists + c.in_deezer_playlists + c.in_apple_playlists)) AS quartile_total_playlist,
   NTILE(4) OVER (ORDER BY t.bpm) AS quartile_bpm,
   NTILE(4) OVER (ORDER BY `danceability_%`) AS quartile_danceability,
   NTILE(4) OVER (ORDER BY `valence_%`) AS quartile_valence,
   NTILE(4) OVER (ORDER BY `energy_%`) AS quartile_energy,
   NTILE(4) OVER (ORDER BY `acousticness_%`) AS quartile_acousticness,
   NTILE(4) OVER (ORDER BY `instrumentalness_%`) AS quartile_instrumentalness,
   NTILE(4) OVER (ORDER BY `liveness_%`) AS quartile_liveness,
   NTILE(4) OVER (ORDER BY `speechiness_%`) AS quartile_speechiness
 FROM
   `laboratoria-426816.proyecto2_hipotesis.track_in_spotify_clean` AS s
 LEFT JOIN
   `laboratoria-426816.proyecto2_hipotesis.track_in_competition_clean` AS c
   ON s.track_id = c.track_id
 LEFT JOIN
   `laboratoria-426816.proyecto2_hipotesis.track_technical_info_clean` AS t
   ON s.track_id = t.track_id
)
SELECT
 q.*,
CASE
   WHEN q.quartile_streams <= 2 THEN 'baja'
   WHEN q.quartile_streams >= 3 THEN 'alta'
   ELSE 'desconocido'
 END AS streams_category,
CASE
   WHEN q.quartile_total_playlist <= 2 THEN 'baja'
   WHEN q.quartile_total_playlist >= 3 THEN 'alta'
   ELSE 'desconocido'
 END AS playlists_category,
 CASE
   WHEN q.quartile_streams >= 3 AND q.quartile_total_playlist >= 3 THEN 'muy alta'
   WHEN q.quartile_streams >= 3 AND q.quartile_total_playlist <= 2 THEN 'alta'
   WHEN q.quartile_streams <= 2 AND q.quartile_total_playlist >= 3 THEN 'moderada'
   WHEN q.quartile_streams <= 2 AND q.quartile_total_playlist <= 2 THEN 'baja'
   ELSE 'desconocido'
 END AS popularity,
 CASE
   WHEN q.quartile_bpm = 1 THEN 'lenta'
   WHEN q.quartile_bpm = 2 THEN 'media'
   WHEN q.quartile_bpm = 3 THEN 'rapida'
   WHEN q.quartile_bpm = 4 THEN 'muy rapida'
   ELSE 'desconocido'
 END AS bpm_category,
 CASE
   WHEN q.quartile_danceability <= 2 THEN 'baja'
   WHEN q.quartile_danceability >= 3 THEN 'alta'
   ELSE 'desconocido'
 END AS danceability_category,
 CASE
   WHEN q.quartile_valence <= 2 THEN 'baja'
   WHEN q.quartile_valence >= 3 THEN 'alta'
   ELSE 'desconocido'
 END AS valence_category,
 CASE
   WHEN q.quartile_energy <= 2 THEN 'baja'
   WHEN q.quartile_energy >= 3 THEN 'alta'
   ELSE 'desconocido'
 END AS energy_category,
 CASE
   WHEN q.quartile_acousticness <= 2 THEN 'baja'
   WHEN q.quartile_acousticness >= 3 THEN 'alta'
   ELSE 'desconocido'
 END AS acousticness_category,
 CASE
   WHEN q.quartile_instrumentalness <= 2 THEN 'baja'
   WHEN q.quartile_instrumentalness >= 3 THEN 'alta'
   ELSE 'desconocido'
 END AS instrumentalness_category,
 CASE
   WHEN q.quartile_liveness <= 2 THEN 'baja'
   WHEN q.quartile_liveness >= 3 THEN 'alta'
   ELSE 'desconocido'
 END AS liveness_category,
 CASE
   WHEN q.quartile_speechiness <= 2 THEN 'baja'
   WHEN q.quartile_speechiness >= 3 THEN 'alta'
   ELSE 'desconocido'
 END AS speechiness_category
FROM
 Quartiles AS q

```
