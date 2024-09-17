# Identificar y manejar datos discrepantes en variables categóricas

<aside>
💡 Limpiar columnas preexistentes o generar columnas nuevas limpias sin caracteres especiales � para “track_name” y “artists_name”. r'[^a-zA-Z0-9]' es el código para el caracter �. Los caracteres quedan reemplazados por un espacio en blanco. Con LOWER dejar todos los strings con letras minúsculas. Con UPPER se pueden dejar todos los string con mayúsculas. Guardar la consulta como track_in_spotify_regexp”.

</aside>

## **Opción 1 (utilizada)**

```sql
SELECT
track_id,
LOWER (REGEXP_REPLACE(track_name, r'[^a-zA-Z0-9]', ' ')) AS track_name,
LOWER (REGEXP_REPLACE(artists_name, r'[^a-zA-Z0-9]', ' ')) AS artists_name,
artist_count, released_day, in_spotify_playlists, in_spotify_charts, streams
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_spotify`
```

<aside>
💡 Reemplaza la columna original por una con datos limpios.

</aside>

## Opción 2

```sql
SELECT *,
LOWER (REGEXP_REPLACE(track_name, r'[^a-zA-Z0-9]', ' ')) AS track_name_limpio,
LOWER (REGEXP_REPLACE(artists_name, r'[^a-zA-Z0-9]', ' ')) AS artists_name_limpio
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_spotify`
```

<aside>
💡 Genera columnas nuevas limpias.

REGEXP es necesario solo en la tabla “track_in_spotify”, ya que es la única que contiene caracteres especiales.

</aside>
