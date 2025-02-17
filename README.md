# Rosa de Viento - Análisis en Colab

## Descripción
Este notebook ejecuta el análisis de la rosa de viento a partir de datos climatológicos. Se utilizan librerías especializadas para la manipulación y visualización de datos.

## Requisitos
Asegúrate de tener instaladas las siguientes librerías antes de ejecutar el notebook:
- `numpy`
- `pandas`
- `matplotlib`
- `windrose`

## <a href="https://colab.research.google.com/github/Bill-Roa/Descargar-ERA5-Colab-Hidrologia/blob/main/Rosa%20de%20viento%20colab.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>


## Uso
Ejecuta las celdas en orden para procesar los datos y generar la rosa de viento.

## Código Principal
```python
```python
%matplotlib inline
import pandas as pd
import numpy as np
from matplotlib import pyplot as plt
import matplotlib.cm as cm
from math import pi
!pip install windrose
from windrose import WindroseAxes

#se pone el nombre del excel de los datos
df = pd.read_excel('Datos_RosadeVientos.xlsx');
df
df['velocidad_x'] = df['VELOCIDAD'] * np.sin(df['DIRECCION'] * pi / 180.0);
df['velocidad_y'] = df['VELOCIDAD'] * np.cos(df['DIRECCION'] * pi / 180.0);
fig, ax = plt.subplots(figsize=(8, 8), dpi=80);
x0, x1 = ax.get_xlim();
y0, y1 = ax.get_ylim();
ax.set_aspect('equal')
_ = df.plot(kind='scatter', x='velocidad_x', y='velocidad_y', alpha=0.1, ax=ax);

#Para cambiar los ejes utilizando "Oeste" en vez de "West"
new_labels = ["E", "N-E", "N", "N-O", "O", "S-O", "S", "S-E"];
ax = WindroseAxes.from_ax(theta_labels=new_labels);

ax.bar(df.DIRECCION, df.VELOCIDAD, normed=True, opening=0.7, edgecolor='white')

#el box_to_anchor cambia (que tan lejos esta hacia los lados, que tan lejos esta hacia abajo) y el loc es en donde quieres que vaya la leyenda
ax.set_legend(
    title="$m \cdot s^{-1}$", bbox_to_anchor=(1.15, -0.1), loc="lower right"
)
```

Para más detalles, revisa el notebook completo.
