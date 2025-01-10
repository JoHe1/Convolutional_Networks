# **Autoencoder: Reducción de Ruido y Reducción/Ampliación de Dimensionalidad en Imágenes**

Este proyecto implementa un Autoencoder usando Redes Neuronales Convolutivas para dos tareas distintas:

**Eliminación de Ruido en Imágenes:** Este modelo es entrenado para eliminar el ruido añadido anteriormente a las imágenes del dataset MNIST.
**Reducción y Ampliación de Dimensionalidad en Imágenes:** Este modelo reduce las dimensiones de las imágenes para representar la información más importante y luego las reconstruye ampliandolas de nuevo. 

Las dos tareas usan el mismo enfoque de Autoencoder, pero con objetivos y configuraciones distintas.

## **Dataset**

El dataset usado es MNIST, un conjunto de datos de imágenes de dígitos escritos a mano. Este dataset contiene 60,000 imágenes de entrenamiento y 10,000 imágenes de prueba, con imágenes de 28x28 píxeles en escala de grises.

## **1. Eliminación de Ruido en Imágenes**

### **Descripción**
En esta parte del proyecto, al principio se añade ruido a las imágenes del dataset MNIST y luego se entrena el Autoencoder para eliminar este ruido añadido. La idea es que el Autoencoder se entrene con imágenes ruidosas como entrada, y las imágenes originales sin el ruido añadido como objetivo, aprendiendo de esta manera a reconstruir las imágenes.

### **Proceso**

**Añadir Ruido:** Generación de ruido aleatorio que se añade a las imágenes del dataset.

**Entrenamiento del Autoencoder:** Se entrena el modelo para minimizar la diferencia entre la imagen original y la reconstruida, eliminando el ruido en el proceso y reconstruyendo la imagen sin el ruido.

**Visualización de los Resultados:** Visualizamos con 5 ejemplos las imágenes originales, las imágenes con ruido y las imágenes reconstruidas por el autoencoder.

### **Resultados**

En el notebook se pueden visualizar los resultados, pero comentando brevemente podemos decir que los resultados obtenidos son satisfactorios. El modelo logra restaurar bien las imágenes originales a partir de las versiones ruidosas, eliminando la mayor parte del ruido añadido, lo cual muestra que tiene una buena capacidad para eliminar el ruido y recuperar los detalles impoertantes de las imágenes originales.

## **2. Superresolución**

### **Descripción**

En esta parte del proyecto lo que se va a hacer es pasar a los autoencoders imagenes de MNIST reducidas a 7x7 y 14x14 para luego reconstruirlas a su tamaño original de 28x28. La idea es que el Autoencoder aprenda a volver a construir la imagen original a partir de una versión reducida de la misma.

### **Proceso**

**Reducción de Resolución:** Utilizando Transformaciones de Pytorch, se reduce la resolución de las imágenes de 28x28 a 7x7 y 14x14 píxeles, para poderlas pasar al Autoencoder.
**Ampliación de Resolución:** El autoencoder se entrena para reconstruir las imágenes originales de 28x28 píxeles a partir de las versiones reducidas de 7x7 y 14x14 píxeles.

Tenemos 2 modelos de Autoencoder, uno para imagenes reduciadas a 7x7 y otro para imagenes reducidas a 14x14, que luego se amplian a 28x28.

### **Resultados**

En el notebook se pueden visualizar los resultados, pero comentándolos brevemente podemos decir que a pesar de la reducción de resolución, el modelo logra reconstruir las imágenes originales con una calidad aceptable, recuperando la mayor parte de los detalles importantes de las imágenes originales.

### **Ejecución del Proyecto**

## **Requisitos**

Es necesario instalar las siguientes bibliotecas antes de ejecutar los notebooks:

- Pythorch
- Matplotlib
- Torchvision

## **Instrucciones de Ejecución**

1. Clonar el repositorio o descargar el notebook
2. Para descagar el dataset y entrenar el autoencoder, solo se necesita ejecutar el notebook paso a paso. En la primera parte del notebook está la parte de eliminación de ruido, y en la segunda la reducción y ampliación de la resolución.