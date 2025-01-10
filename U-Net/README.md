# **U-Net para Segmentación de Imágenes**

Este proyecto implementa el modelo U-Net, que es una red neuronal convolutiva diseñada para tareas de segmentación de imágenes. La arquitectura U-Net incluye una parte de contracción y una parte de expansión, llamados encoder y decoder respectivamente, con conexiones de salto que permiten guardar información de alta resolución de la imagen de entrada. El modelo se entrena para segmentar objetos, en este caso monedas, separándolos del resto de la imagen.

## **Datos**

El conjunto de datos utilizado contiene imágenes de monedas sobre superficies y sus respectivas máscaras. Primero las imágenes se redimensionan a 512x512 píxeles y se normalizan en el rango [0, 1]. Para ello implementamos una clase personalizada DatasetU_Net para cargar las imágenes y máscaras, y usamos DataLoader para manejar los lotes de datos durante el entrenamiento y prueba.

## **Pruebas realizadas**

**La práctica consta de dos partes, por lo que realizamos 2 pruebas con el Modelo**

**Reducción progresiva de canales:** Generamos distintos modelos, reduciendo progresivamente los números de canales de las capas convolutivas en el encoder y decoder, y envaluamos el impacto en la precisión del modelo. La reducción progresiva la hicimos dividiendo los valores a la mitad cada vez que generamos el siguiente modelo, y esto lo repetimos hasta que notamos que empezaba a empeorar el resultado, que fue con el tercer modelo, que empieza con 16 canales.

**Eliminación progresiva de conexiones de salto:** Cogimos el modelo donde empezamos a notas más fallos, que era el de 16 canales de entrada, y le aplicamos la eliminación progresiva de conexiones de salto (skips), eliminando con cada modelo uno para ver cómo afectaba a los resultados del modelo.

## **Implementación del Modelo**

El modelo se construye con bloques convolucionales, bloques de codificación y bloques de decodificación,llamados encoder y decoder respectivamente. El encoder se encarga de reducir la resolución de las imágenes, mientras que el decoder a su vez aumenta la resolución de las imágenes. Junto a eso, se implementaron conexiones de salto (skips) para concatenar información del encoder al decoder, es decir que siempre incluya una parte de la imagen original para que aprenda mejor.

## **Ejecución del proyecto**

### **1. Instalar dependencias**

Para ejecutar el proyecto hacen falta estas librerías: 

- Numpy
- Torch
- Torchvision
- Matplotlib

### **2. Preparar los datos**

Descargar o copiar el notebook.

Descargar las imágenes y colocarlas con sus máscaras en las carpetas correspondientes: las imágenes de entrada en el directorio imagenes y las mascaras asociadas en el directorio labels, y para la prueba, las respectivas imágenes deben estar en el directorio test. 


### **3. Ejecutar el entrenamiento**

Para entrenar el modelo, simpelmente debe ejecutar el notebook en orden. Primero se reducirán los números de canales, y luego los skips.

### **4. Ver los resultados**

El código de entrenamiento genera y guarda automáticamente los modelos entrenados en archivos .pth, que luego se volverán a cargar en el apartado de visualización del código, cada gráfico presenta la imagen original y la mascara segmentada predicha por el modelo.

## **Resultados**

Ahora expondremos los resultados que obtuvimos de las dos pruebas y lo que observamos con cada uno:

### **1. Reducción Progresiva de Canales**
En esta parte, como explicado anteriormente, entrenamos los modelos con distintos números de canales en las capas, empezando con un modelo de 64 canales base, reduciendo en cada modelo a la mitad el número de canales. Eso lo hicimos 3 veces (llegando a un modelo de 16 canales base) ya que tras la tercera iteración ya notamos que empeoraba bastante, por lo que lo dejamos en esa para empezar a quitarle los skips a ese modelo en la siguiente prueba.

**Modelo 1 (base_channels = 64)**
En las imagenes resultantes de este modelo podemos ver que las monedas se detectan correctamente en las 4 imágenes, representando su forma de manera bastante precisa en casi todos los casos, sin errores significativos ni valores atípicos.

**Modelo 2 (base_channels = 32)**
En este modelo, aunque la precisión disminuye ligeramente, la diferencia no es importante. Los círculos que representan las monedas siguen siendo relativamente pequeños y bien definidos, aunque un poco menos suaves. En algunos casos, se empiezan a observar pequeños errores en las formas, pero siguen detectándose las monedas correctamente en su mayoría.

**Modelo 3 (base_channels = 16)**
En este modelo, los errores son más evidentes. La máscara muestra manchas en áreas donde no hay monedas, y los círculos que representan las monedas ya no están tan definidos. Dado que los resultados muestran más imprecisiones, utilizaremos este modelo como base para eliminar las conexiones de salto.


**2. Eliminación Progresiva de Conexiones de Salto**

Como explicamos anteriormente, en esta prueba cogimos el modelo donde tras reducir el numero de canales vimos que ya empezaba a empeorar más (base_channels = 16) y empezamos a eliminarle progresivamente las conexiones de salto en el decoder uno a uno, creando un modelo con cada caso.

**Modelo con 3 conexiones de salto**
Con 3 conexiones de salto, el modelo muestra más errores en las formas de las monedas, que ya no se ven tan definidas. Además, se observan pequeños errores dentro de las monedas, y las formas de las monedas son algo imperfectas.

**Modelo con 2 conexiones de salto**
En este modelo, no se observan grandes diferencias. En algunos casos, los errores del modelo anterior han mejorado. Sin embargo, las formas de las monedas son menos definidas, ya que tienen menos esquinas.

**Modelo con 1 conexión de salto**
En este modelo, los errores son más graves. Las formas de las monedas están mucho menos definidas y presentan errores significativos en su interior.

**Modelo sin conexiones de salto**
En este último modelo, sin conexiones de salto, los resultados son similares a los anteriores, pero más pronunciados. Las formas de las monedas ya no están definidas en absoluto y se mezclan entre sí, por lo que ya no se puede identificar que son monedas.

## **Conclusión**

Los resultados obtenidos en estas pruebas muestran que la reducción de canales y la eliminación de conexiones de salto impactan significativamente en la precisión del modelo. A medida que se reducen los canales o se eliminan los saltos, la precisión disminuye y la máscara segmentada muestra más imperfecciones, especialmente al identificar las monedas. Sin embargo, algunos experimentos demostraron que el modelo aún puede funcionar bien con menos canales o sin algunas conexiones de salto. Esto sugiere que el rendimiento del modelo depende de un equilibrio entre ambos factores, y que si hace falta priorizar la optimización, se puede reducir el número de canales o las conexiones de salto y seguirán siendo buenos resultados si se mantiene un buen equilibrio. 