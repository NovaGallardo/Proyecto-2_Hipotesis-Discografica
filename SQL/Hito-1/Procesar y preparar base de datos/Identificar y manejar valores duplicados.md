## Identificar valores duplicados en “track_in_spotify_null”

```sql
SELECT artists_name, track_name, COUNT(*) AS veces_repetido, ARRAY_AGG(track_id) AS track_ids, ARRAY_AGG(streams) AS streams
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_spotify`
WHERE artists_name IS NOT NULL AND track_name IS NOT NULL
GROUP BY artists_name, track_name
HAVING COUNT(*) > 1
```

<aside>
💡 **Se encontraron 4 canciones duplicadas, cada una con dos ID distintos.**

Guardar consulta como “track_in_spotify_duplicates” con “Guardar la consulta (versión clásica)”.

Descargar consulta en .csv y Hoja de Cálculos.

</aside>

![unnamed (2).png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ebb9ff67-9568-4153-82ed-51e9dbc8b9ad/65ed8da6-2c72-446e-ab11-723e939e4301/unnamed_(2).png)

Decidimos dejar la versión que tenga más streams. En el caso de Rosa Linn es la de ID 5675634, para Lizzo cualquiera de las dos (ambas tienen igual cantidad de streams), para The Weeknd el ID 4586215, para ThxSoMch el ID 4967469.

## Identificar valores duplicados en “track_in_competition”

```sql
SELECT track_id
FROM laboratoria-426816.proyecto2_hipotesis.track_in_competition
WHERE track_id IS NOT NULL
GROUP BY track_id
HAVING COUNT (*) > 1
```

<aside>
💡 No se encontraron duplicados.

</aside>

## Identificar valores duplicados en “track_technical_info”

```sql
SELECT track_id
FROM laboratoria-426816.proyecto2_hipotesis.track_technical_info
WHERE track_id IS NOT NULL
GROUP BY track_id
HAVING COUNT (*) > 1
```

<aside>
💡 No se encontraron duplicados.

</aside>
