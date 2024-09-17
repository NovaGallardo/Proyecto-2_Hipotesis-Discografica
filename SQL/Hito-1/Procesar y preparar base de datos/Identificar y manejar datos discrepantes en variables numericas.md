# Identificar y manejar datos discrepantes en variables numéricas

<aside>
💡 Al realizar query con MIN, MAX y AVG en “track_in_spotify” se detecta que hay una celda de la columna ”streams” que contiene valores cualitativos y cuantitativos, siendo que deberían ser solo datos cuantitativos (cantidad de streams). La variable debería ser INTEGER pero está como STRING. Arroja el siguiente error: “No matching signature for aggregate function AVG for argument types: STRING. Supported signatures: AVG(INT64); AVG(FLOAT64); AVG(NUMERIC); AVG(BIGNUMERIC); AVG(INTERVAL) at [4:1] “.

</aside>

```sql
SELECT 
MIN(streams),
MAX(streams),
AVG(streams)
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_spotify`
```

<aside>
💡 **La fila 47 contiene el error.** La celda tiene la siguiente información: BPM110KeyAModeMajorDanceability53Valence75Energy69Acousticness7Instrumentalness0Liveness17Speechiness3. Realizar el siguiente punto y luego regresar a este.

</aside>

```sql
SELECT
MIN(SAFE_CAST(streams AS INT64)) AS streams_min,
MAX(SAFE_CAST(streams AS INT64)) AS streams_max,
AVG(SAFE_CAST(streams AS INT64)) AS streams_avg
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_spotify`
WHERE
 SAFE_CAST(streams AS INT64) IS NOT NULL
```

<aside>
💡 **Resultados:**

streams_min 	2762

streams_max 	3703895074

streams_avg 	514137424.93907595

**Actualizar query “track_in_spotify_min_max_avg” para sobreescribir datos de la query anterior.**

</aside>
