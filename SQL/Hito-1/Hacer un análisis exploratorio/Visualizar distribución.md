# Visualizar distribución

<aside>
💡 Crear histogramas para bpm, streams_int y total_playlists. Insertar el siguiente código en el editor de scripts de Python

</aside>

```python
# Obtén los datos de Power BI - solo necesita cambiar esta información de todo el código
data = dataset[['SU VARIABLE']]# Crea el histograma
plt.hist(data, bins=10, color='blue', alpha=0.7)
plt.xlabel('Valor')
plt.ylabel('Frecuencia')
plt.title('Histograma')# Muestra el histograma
plt.show()
```
