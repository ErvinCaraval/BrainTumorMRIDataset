# Brain Tumor MRI Dataset - Pipeline de preprocesamiento y entrenamiento

Este proyecto está orientado a la detección de tumores cerebrales en imágenes MRI usando modelos de visión por computadora. El flujo principal incluye:

- preprocesamiento de imágenes y máscaras,
- generación de anotaciones en formato YOLO y Pascal VOC,
- entrenamiento de YOLOv8,
- entrenamiento de Faster R-CNN,
- comparación de ambos modelos con métricas como precisión, recall, IoU y mAP.

El proyecto está diseñado para ejecutarse principalmente en Google Colab, porque los notebooks asumen que el dataset y los resultados se almacenan en Google Drive.

## Estructura del proyecto

- DATASET/: carpeta original con los datos de entrada del problema.
- Notebooks/: notebooks principales del proyecto.
  - braintumorpreprocessing.ipynb: preprocesamiento del dataset y generación del dataset listo para entrenamiento.
  - YOLOv8_Training.ipynb: entrenamiento del modelo YOLOv8.
  - Faster_RCNN_Training.ipynb: entrenamiento del modelo Faster R-CNN.
  - Comparacion_YOLOv8_vs_FasterRCNN.ipynb: comparación de ambos modelos.
- Processed_Dataset/: dataset preparado para entrenamiento con carpetas de imágenes, etiquetas y archivo dataset.yaml.
- outputs/: resultados generados por los entrenamientos y comparaciones.

## Requisitos

Este proyecto usa bibliotecas de visión por computadora y aprendizaje profundo. En Colab, lo más común es ejecutar con:

- Python 3.10 o 3.11
- GPU opcional, aunque el flujo también puede correr en CPU con ajustes de batch size y tamaño de imagen.
- Google Drive montado para acceder al dataset y guardar resultados.

## Flujo recomendado en Google Colab

### 1. Montar Google Drive

Ejecuta al inicio de cada notebook:

```python
from google.colab import drive
drive.mount('/content/drive')
```

Se espera que el proyecto esté en una ruta similar a:

```python
/content/drive/MyDrive/BrainTumorMRIDataset
```

### 2. Ejecutar el preprocesamiento

Abre y ejecuta el notebook:

- Notebooks/braintumorpreprocessing.ipynb

Este notebook:

- lee las imágenes y máscaras desde DATASET/Segmentation,
- selecciona imágenes sin tumor de forma proporcional,
- divide los datos en train/val/test,
- genera imágenes procesadas y anotaciones en formato YOLO y Pascal VOC,
- guarda el resultado en Processed_Dataset/.

### 3. Entrenar YOLOv8

Luego ejecuta:

- Notebooks/YOLOv8_Training.ipynb

Este notebook espera que exista el archivo:

- Processed_Dataset/dataset.yaml

Y guarda los resultados en:

- outputs/Resultados_YOLOv8

### 4. Entrenar Faster R-CNN

Luego ejecuta:

- Notebooks/Faster_RCNN_Training.ipynb

Este notebook usa el mismo dataset procesado y guarda los resultados en:

- outputs/Resultados_Faster_RCNN

### 5. Comparar ambos modelos

Una vez que ambos entrenamientos hayan terminado, ejecuta:

- Notebooks/Comparacion_YOLOv8_vs_FasterRCNN.ipynb

Este notebook lee los resultados previos y genera gráficas y métricas comparativas en:

- outputs/Resultados_Comparacion

## Archivos importantes generados

Tras ejecutar el flujo completo, el proyecto espera generar carpetas como estas:

- Processed_Dataset/images/train
- Processed_Dataset/images/val
- Processed_Dataset/images/test
- Processed_Dataset/annotations_voc/train
- Processed_Dataset/annotations_voc/val
- Processed_Dataset/annotations_voc/test
- outputs/Resultados_YOLOv8
- outputs/Resultados_Faster_RCNN
- outputs/Resultados_Comparacion

## Dependencias principales

Las bibliotecas más importantes usadas por el proyecto son:

- torch
- torchvision
- ultralytics
- opencv-python
- numpy
- pandas
- matplotlib
- scikit-learn
- Pillow
- albumentations
- torchmetrics

## Notas importantes

- Los notebooks están escritos con rutas orientadas a Google Colab y Google Drive.
- Si vas a ejecutar el proyecto localmente, deberás adaptar las rutas de acceso al dataset y a los resultados.
- Para entrenamientos más estables en CPU, conviene bajar el batch size y el tamaño de imagen.
- Si no tienes GPU, puedes seguir el flujo, pero los tiempos de entrenamiento serán más largos.

## Resumen corto de ejecución

1. Subir o conectar el proyecto a Google Drive.
2. Montar Drive en Colab.
3. Ejecutar braintumorpreprocessing.ipynb.
4. Ejecutar YOLOv8_Training.ipynb.
5. Ejecutar Faster_RCNN_Training.ipynb.
6. Ejecutar Comparacion_YOLOv8_vs_FasterRCNN.ipynb.

## Detección de problemas comunes

- Si aparece un error de rutas, revisa que la carpeta del proyecto esté montada en Drive con el mismo nombre.
- Si no existe Processed_Dataset, probablemente el preprocesamiento no terminó correctamente.
- Si el entrenamiento falla por memoria, reduce batch size o imagenes de entrada.
- Si no aparece el modelo entrenado, revisa la carpeta de resultados esperada.
