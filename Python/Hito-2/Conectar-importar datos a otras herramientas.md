Ir a Google Colab https://colab.research.google.com/ y en la ventana “Abrir bloc de notas” dar click en “+ Nuevo notebook”. Asignarle título “proyecto2_hito2.ipynb”.

Obtener un .xlsx de la tabla “track_all_data” de Big Query. En Big Query seleccionar la vista “track_all_data” y dar click en “Exportar” > “Explorar como Hojas de Cálculo”. Una vez que se abre la tabla en Google Sheets, exportarla en formato .xlsx.

En Google Colab correr el siguiente código:

```python
from google.colab import files
load=files.upload() #seleccionar el archivo .xlsx
import pandas as pd
data=pd.read_excel(load['track_all_data.xlsx'])
data.head() #previsualizar tabla
```
