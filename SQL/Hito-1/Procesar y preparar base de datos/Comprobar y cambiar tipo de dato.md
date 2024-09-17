# Comprobar y cambiar tipo de dato

<aside>
💡 CAST nos permite asignar un tipo de dato a una columna determinada. En este caso determinamos que la columna “streams” correponderá a INTEGER (valores numéricos enteros). SAFE_CAST devuelve como nulos los valores que no correspondan al tipo de dato asignado (en este caso si hay un STRING en lugar de INTEGER). Con IS NOT NULL especificamos que filtre los valores que resulten nulos.

</aside>

```sql
SELECT
 SAFE_CAST(streams AS INT64) AS streams
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_spotify`
WHERE
 SAFE_CAST(streams AS INT64) IS NOT NULL
```

Guardar consulta como “track_in_spotify_CAST”.
