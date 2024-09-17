# Crear nuevas variables

<aside>
💡 Usar CONCAT para unir “released_year”, “released month y released_day” separadas por guión en nueva columna “released_date”, asignándole formato DATE (fecha) con CAST.

</aside>

```sql
SELECT
 CAST(CONCAT(released_year, '-', released_month, '-', released_day) AS DATE) AS released_date
FROM `laboratoria-426816.proyecto2_hipotesis.track_in_spotify`
```

Guardar consulta como “track_in_spotify_released_date”.
