# **Proyectos de Aprendizaje Automático 2**

Este repositorio consta de tres proyectos implementados con redes neuronales para diferentes tareas de procesamiento y análisis de imágenes. Cada proyecto utiliza un enfoque distinto, abarcando desde clasificación de imágenes, eliminación de ruido, hasta segmentación de imágenes. Están basados en modelos avanzados como Redes Neuronales Convolutivas, Autoencoders y U-Net. 

## **1. Redes Neuronales Convolutivas para la Detección de Animales**

El objetivo de este proyecto es desarrollar un modelo robusto para la clasificación de imágenes de animales usando Redes Neuronales Convolutivas, implementando distintos enfoques y optimizaciones:

**Dataset:** Utiliza el conjunto de datos "Animal Image Dataset (90 Different Animals)" de Kaggle, reducido a 7 clases: Cisne, Tigre, Pavo, Lobo, Wombat, Cebra y Pájaro Carpintero.

**Modelos:**
Red CNN Clásica: Entrenamiento de una red convolutiva básica para la clasificación de 7 clases de animales.

Optuna para Optimización de Hiperparámetros: Optimización automática de los hiperparámetros del modelo utilizando Optuna.

Transfer Learning con VGG16: Uso del modelo preentrenado VGG16 para mejorar el rendimiento en la clasificación.

## **2. Autoencoder para la Reducción de Ruido y Reducción/Ampliación de Dimensionalidad en Imágenes**

En este proyecto se implementa un Autoencoder usando Redes Neuronales Convolutivas para realizar dos tareas:

**Eliminación de Ruido en Imágenes:** El modelo aprende a eliminar el ruido añadido a las imágenes del dataset MNIST.

**Reducción y Ampliación de Dimensionalidad:** El modelo reduce la resolución de las imágenes y luego las amplía, manteniendo las características clave.

**Dataset:** El conjunto de datos MNIST, con imágenes de dígitos escritos a mano.

## **3. U-Net para Segmentación de Imágenes**

En este proyecto se implementa un modelo U-Net para la segmentación de imágenes de monedas, con el objetivo de separar las monedas de las imágenes del fondo.

**Dataset:** Imágenes de monedas con sus respectivas máscaras.

**Pruebas:**
Reducción Progresiva de Canales: Se reduce el número de canales en las capas convolutivas para evaluar el impacto en la precisión.

Eliminación Progresiva de Conexiones de Salto: Se eliminan las conexiones de salto en el modelo para analizar su influencia en el rendimiento.

## **Instrucciones Generales**

**1. Instalación de Dependencias**
Instalar las bibliotecas necesarias para cada proyecto.

**2. Preparar los Datos**
Descargar los datasets correspondientes y colócalos en las rutas adecuadas según las instrucciones de cada proyecto.

**3. Ejecución de los Proyectos**
Clonar o descargar los notebooks.
Ejecutar los notebooks paso a paso para entrenar y evaluar los modelos.
