# Proyecto FFT para Procesamiento de Imágenes

Este proyecto corresponde al primer entregable de Análisis Numérico: un cuaderno de Jupyter donde se estudia el uso de la Transformada Rápida de Fourier (FFT) aplicada al procesamiento de imágenes, específicamente para analizar desenfoque, energía de altas frecuencias y filtros en el dominio de Fourier.

El archivo principal del proyecto es:

```text
procesamineto-de-imagenes-fft.ipynb
```

## 1. Objetivo del notebook

El cuaderno permite:

- Cargar una imagen propia.
- Convertirla a escala de grises.
- Calcular la FFT 2D de la imagen.
- Visualizar el espectro de magnitud en el dominio de frecuencias.
- Aplicar desenfoque gaussiano con distintos valores de sigma.
- Analizar cómo el desenfoque reduce la energía de altas frecuencias.
- Implementar una métrica de detección de desenfoque usando FFT.
- Comparar el comportamiento de la FFT con la varianza del Laplaciano.
- Aplicar filtros pasa bajas y pasa altas en el dominio de frecuencias.

## 2. Requisitos previos

Antes de ejecutar el notebook, asegúrate de tener instalado:

- Python 3.10 o superior.
- Visual Studio Code, Jupyter Notebook, JupyterLab o Anaconda.
- Extensión de Python en VS Code, si se trabaja desde VS Code.
- Extensión de Jupyter en VS Code, si se trabaja desde VS Code.
- Conexión a internet para instalar las librerías.

## 3. Librerías necesarias

El notebook utiliza las siguientes librerías de Python:

```text
numpy
matplotlib
pandas
scikit-image
opencv-python
pillow
jupyter
```

Estas librerías permiten trabajar con arreglos numéricos, gráficos, imágenes, tablas y ejecución del cuaderno.

## 4. Estructura recomendada del proyecto

Se recomienda organizar los archivos de la siguiente manera:

```text
proyecto_fft/
│
├── proyecto_fft_imagenes_notebook.ipynb
├── README.md
│
└── data/
    ├── imagen_nitida.jpg
    ├── imagen_borrosa.jpg
    └── documento.jpg
```

La carpeta `data` debe estar en el mismo directorio donde se encuentra el notebook.

## 5. Instalación

### Opción A: instalación directa

Abre una terminal en la carpeta del proyecto y ejecuta:

```bash
python -m pip install numpy matplotlib pandas scikit-image opencv-python pillow jupyter
```

Si el comando anterior no funciona en Windows, prueba con:

```bash
py -m pip install numpy matplotlib pandas scikit-image opencv-python pillow jupyter
```

### Opción B: instalación con entorno virtual

Esta opción es más ordenada porque mantiene las librerías del proyecto separadas del resto del sistema.

Primero, crea el entorno virtual:

```bash
python -m venv .venv
```

En Windows, actívalo con:

```bash
.venv\Scripts\activate
```

En Linux o macOS, actívalo con:

```bash
source .venv/bin/activate
```

Luego instala las dependencias:

```bash
python -m pip install numpy matplotlib pandas scikit-image opencv-python pillow jupyter
```

Si trabajas en VS Code, selecciona el kernel correspondiente a `.venv` desde la parte superior derecha del notebook.

## 6. Verificación de instalación

Antes de ejecutar todo el notebook, puedes probar esta celda:

```python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
import cv2
from skimage import io, data, color
from PIL import Image

print("Librerías cargadas correctamente")
```

Si no aparece ningún error, la instalación fue correcta.

## 7. Uso del notebook

### Paso 1: colocar imágenes de prueba

Crea una carpeta llamada `data` en la raíz del proyecto.

Luego coloca dentro una o más imágenes, por ejemplo:

```text
data/imagen_nitida.jpg
data/imagen_borrosa.jpg
data/documento.jpg
```

### Paso 2: configurar la ruta de la imagen

En el notebook, busca la celda donde se define la ruta de la imagen y cambia el nombre del archivo según la imagen que quieras probar:

```python
ruta_imagen = "data/imagen_nitida.jpg"
```

Si quieres probar otra imagen, cambia la ruta:

```python
ruta_imagen = "data/imagen_borrosa.jpg"
```

### Paso 3: ejecutar las celdas en orden

Ejecuta las celdas del notebook desde arriba hacia abajo.

El cuaderno mostrará:

- Imagen original en escala de grises.
- Espectro de magnitud de la FFT.
- Comparaciones con diferentes niveles de desenfoque.
- Tabla de resultados.
- Gráfica de energía de altas frecuencias.
- Filtros pasa bajas y pasa altas.
- Comparación con la varianza del Laplaciano.

## 8. Ajuste del umbral FFT

El notebook clasifica una imagen como borrosa o no borrosa usando una métrica basada en la media de altas frecuencias.

La regla general es:

```python
borrosa = media_fft <= umbral
```

En algunas imágenes, especialmente cuando están normalizadas entre `0` y `1`, la métrica puede dar valores negativos. En ese caso, un umbral positivo como `10` puede hacer que todas las imágenes se clasifiquen como borrosas.

Para imágenes normalizadas, puedes probar umbrales como:

```python
umbrales = [-85, -84, -83, -82, -81, -80]
```

Ejemplo:

```python
umbral = -83
```

El umbral debe calibrarse según el tipo de imagen, su escala y la cantidad de textura o bordes presentes.

## 9. Recomendaciones para las imágenes de prueba

Para obtener mejores resultados experimentales, se recomienda usar imágenes con diferentes características:

- Una imagen claramente nítida.
- Una imagen claramente borrosa.
- Una imagen de texto o documento.
- Una imagen con muchos bordes, como edificios, teclado, cuaderno o calle.
- Una imagen con poco detalle, como cielo o fondo liso.

Las imágenes con mucho fondo uniforme pueden tener baja energía de altas frecuencias aunque algunos objetos estén enfocados. Esto debe mencionarse como una limitante del método.

## 10. Problemas comunes

### Error: `ModuleNotFoundError: No module named 'matplotlib'`

Significa que faltan librerías en el entorno actual. Ejecuta:

```bash
python -m pip install matplotlib
```

O instala todas las dependencias:

```bash
python -m pip install numpy matplotlib pandas scikit-image opencv-python pillow jupyter
```

### Warning: `La importación skimage no se ha podido resolver`

Significa que falta instalar `scikit-image`:

```bash
python -m pip install scikit-image
```

### El notebook sigue mostrando errores aunque instalé las librerías

Puede ocurrir si VS Code está usando otro kernel de Python.

Solución:

1. Abre el notebook.
2. Ve a la esquina superior derecha.
3. Haz clic en el kernel actual.
4. Selecciona el Python o entorno virtual donde instalaste las librerías.
5. Reinicia el kernel.

### Todas las imágenes salen como borrosas

Esto puede pasar por dos razones:

1. El umbral no está calibrado para la escala de la imagen.
2. La imagen tiene mucho fondo uniforme y pocos bordes.

Prueba con umbrales negativos o usa imágenes con más textura.

## 11. Interpretación esperada de los resultados

Cuando se aplica desenfoque gaussiano con valores crecientes de `sigma`, se espera que la energía de altas frecuencias disminuya.

Ejemplo esperado:

```text
sigma = 0  → mayor energía de altas frecuencias
sigma = 1  → disminución leve
sigma = 2  → disminución mayor
sigma = 4  → imagen más borrosa
sigma = 8  → fuerte pérdida de detalle
```

Esto ocurre porque las altas frecuencias representan cambios bruscos de intensidad, bordes y detalles finos. Al desenfocar una imagen, esos detalles se suavizan.