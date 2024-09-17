# Construir tablas auxiliares

<aside>
💡 Con WITH y COUNT crear tabla temporal que contenga la cantidad de canciones por artista solista (canciones que no son colaboraciones con otrxs artistas).

</aside>

```sql
WITH solo_artists AS (
 SELECT
   artists_name_clean,
   COUNT(*) AS total_songs
 FROM
   `laboratoria-426816.proyecto2_hipotesis.track_all_data`
 WHERE
   artist_count = 1
 GROUP BY
   artists_name_clean
)
SELECT *
FROM solo_artists
```
