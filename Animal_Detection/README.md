# **Redes Neuronales Convolutivas para la Detección de Animales**

La idea de este proyecto es buscar desarrollar un modelo robusto para la clasificación de imágenes de animales usando Redes Neuronales Convolutivas, implementando distintos enfoques. Mediante el uso de PyTorch, se entrenan modelos, optimizando los hiperparámetros con Optuna y se emplea transfer learning con el modelo preentrenado VGG16.

Todo se explica de forma detallada en los notebooks proporcionados.


## **Dataset utilizado**

Utilizaremos el dataset de Kaggle llamado "Animal Image Dataset (90 Different Animals)
" que contiene 5400 imagenes de 90 clases diferentes de animales. El dataset se encuentra en el siguiente enlace: https://www.kaggle.com/datasets/iamsouravbanerjee/animal-image-dataset-90-different-animals

Para que sea más sencillo para el proyecto, se ha decidido reducir el número de clases a 7. Cada clase incluye alrededor de 60 imágenes distintas del animal correspondiente, los cuales son los siguientes:

Cisne (Swan)

Tigre (Tiger)

Pavo (Turkey)

Lobo (Wolf)

Wombat (Wombat)

Cebra (Zebra)

Pájaro Carpintero (Woodpecker)

El enlace para 


## **Archivos del Proyecto**

### **1. Red_Convolutiva_Deteccion_Animales.ipynb**

Este notebook entrena una red convolutiva clásica que clasifica 7 clases de animales.

**Estructura de la red:**

3 capas convolutivas con funciones de activación Leaky ReLU.

Capas densas para la clasificación final con funciones de activación ReLU

Dropout y MaxPooling para mejorar la generalización.

Valores de los hiperparámetros ajustustados a los resultados de Optuna.

**Entrenamiento:**

Optimizador: Adam

Función de pérdida: CrossEntropyLoss

Parada temprana implementada.

**Evaluación del Modelo:**

Gráficas de precisión y pérdida del entrenamiento y de las pruebas.

Matriz de confusión para evaluar el rendimiento por clase.

**Resultados**

Los resultados se explican y muestran más detalladamente en el notebook, pero podemos decir que la precisión en general aumenta poco a poco y controladamente evitando el sobreajuste, y que tiene una buen desempeño en la clasificación, con una precisión del conjunto de test de 90.58%.

### **2. Red_Convolutiva_Deteccion_Animales_Optuna.ipynb**

Este notebook implementa Optuna para optimizar automáticamente los hiperparámetros de la red convolutiva, y encontrar los que mejores resultados dan para usarlos en la red neuronal convolutiva clásica en el notebook explicado anteriormente. Se utiliza para encontrar la configuración óptima de hiperparámetros antes de entrenar el modelo completo.

**Hiperparámetros optimizados:**

Tamaño del lote.

Tasa de aprendizaje.

Arquitectura de la red (número de filtros, neuronas y funciones de activación).

Dirección de optimización: Maximizar la precisión del modelo.

Se implementaron estrategias como pruning para ahorrar tiempo.

### **3. Red_Convolutiva_Transfer_Learning_VGG16.ipynb**

Este notebook se utiliza si se desea un modelo rápido y efectivo basado en transfer learning. La idea es aplicar un modelo preentrenado a un problema distinto al original. En este caso usamos el modelo VGG16, que fue entrenado previamente en grandes bases de datos de imágenes, para clasificar nuestro dataset de imágenes de animales, con el objetivo de aprovechar las capacidades de extracción de características del VGG16 para mejorar el rendimiento en general.

**Flujo del Código:**

Verificación de GPU, para ver si hay una GPU disponible para acelerar el proceso de entrenamiento (CUDA), lo cual mejora el rendimiento bastante.

Carga de Datos, aplicando data augmentation y dividiendo en 80% para entrenamiento y 20% para la prueba.

Carga del Modelo Preentrenado VGG16 y ajuste de la última capa, adaptándolo al número de clases de nuestro dataset.

Entrenamiento de modelo usando el optimizador SGD (Descenso Gradiente Estocástico). 

Evaluación del modelo mediante la precisión de las predicciones.

**Resultados:**

Este modelo aumenta bastante la precisión, con un valor final de 97.65%.

## **Ejecución del Proyecto**

### **Requisitos**

Es necesario instalar las siguientes bibliotecas antes de ejecutar los notebooks:

- torch 
- torchvision
- scikit-learn 
- matplotlib 
- numpy 
- optuna

## **Instrucciones de Ejecución**

**Preparar el entorno:**

1. Clonar el repositorio o descargar los notebooks.

2. Descargar el dataset desde el enlace proporcionado y colocarlo en una carpeta accesible por los notebooks, actualizando la ruta con la elegida para poder leerlo correctamente.

**Ejecutar los notebooks:**

3. Abre cada notebook en Jupyter Notebook o Jupyter Lab, y ve ejecutando en orden todas las celdas de código de los notebooks para entrenar y evaluar los modelos.

