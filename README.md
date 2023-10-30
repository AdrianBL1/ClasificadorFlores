# Clasificador de Flores
<p align="center">
   <img src="/md/tfl_logo.png" data-canonical-src="md/tfl_logo.png" alt="Logotipo"/>
</p>

Modelo Clasificador de Flores.

Desarrollo de Modelo y Aplicación móvil en Android (Android y Koltin) implementando un clasificador de flores.

## Objetivo

* Diseño  de una red neuronal que reconozca flores endémicas de una región en concreto.
* Creación del modelo y exportalo para su implementación en una aplicación móvil.

## Desarrollo

Modelo

La plataforma de entrenamiento utilizada para entrenar nuestro clasificador de imágenes personalizado es la máquina de enseñanza con Google, [Teachable Machine](https://teachablemachine.withgoogle.com/). Esta es una
plataforma utilizada para el proceso de entrenamiento de aprendizaje
profundo con solo unos pocos clics. 

Procedimiento

Primero, cargando las diferentes clases de objetos de su sistema o usando una cámara web, luego entrenándolo. Finalmente, después de la capacitación, puede exportar el modelo de su elección. Se puede elegir el formato que desee y descargar el modelo. Se estará entrenando un modelo para la clasificación de
imágenes de máscaras.

![Procedimieto](https://cdn-images-1.medium.com/max/2000/0*-dV9UFJJLgIadKgH.png "Procedimieto")

Requerimientos
* El conjunto de datos de imagen de objeto personalizado con diferentes clases.
* Android Studio 3.2 + (instalado en una máquina Linux, Mac o Windows).
* Dispositivo Android en modo desarrollador con depuración USB habilitada.
* Un cable USB (para conectar el dispositivo Android a la computadora).

## Desarrollo

1. Se tomó el conjunto de datos.
2. Se toma el conjunto de imágenes a utilizar.
   <p align="center">
      <img src="/md/muestra_imgs.png" data-canonical-src="/md/muestra_imgs.png" alt="Conjunto de Imágenes" align="center"/> (Referencia)
   </p>
3. Se clasifican en carpetas las imágenes que se vayan a utilizar y el tipo de flor al que corresponden.
   <p align="center">
      <img src="/md/clasific_imgs.png" data-canonical-src="/md/clasific_imgs.png" alt="Clasificación de las Imágenes por Carpetas" align="center"/> (Referencia)
   </p>
4. En Teachable Machine se cargaron las imágenes dividiéndolas en clasificaciones, asignándoles una etiqueta que corresponderá el nombre de las flores que corresponda.
   
   Entre más flores o imágenes se tenga por clase mucho mejor, es importante que en cada clase las imágenes de las flores a utilizar correspondan precisamente al tipo de la clase, porque sino se pueden generar errores en la clasificación de las imágenes.

   <p align="center">
      <img src="/md/tm_clasific.png" data-canonical-src="md/tm_clasific.png" alt="Clasificación de las Imágenes en Teachable Machine" align="center"/> Imágenes divididas por clases.
   </p>

5. Una vez teniendo todas las clases se empieza el entrenamiento del modelo.
   
   Durante el entrenamiento, puede ajustar los hiperparámetros como:
   
   * Nº de épocas.
   * Tamaño del lote.
   * Tasa de aprendizaje.

   <p align="center">
      <img src="/md/tm_ajuste.png" data-canonical-src="/md/tm_ajuste.png" alt="Ajuste del modelo"/>
   </p>

6. Se realiza el entrenamiento.
7. Se verifican resultados del entrenamiento previo.
   
   Se puede obtener una vista previa del modelo entrenado en la ventana vista previa. 
   
   <p align="center">
      <img src="/md/tm_vista_prev.png" data-canonical-src="/md/tm_vista_prev.png" alt="Resultados de entrenamiento"/>
   </p>

8. Exportación.
   
   Comprobados los resultados hayan sido obtimos, se procedió a exportar el modelo.

   <p align="center">
      <img src="/md/tm_export.png" data-canonical-src="/md/tm_export.png" alt="Exportación del modelo"/>
   </p>
   
   Es necesario que el modelo se exporte como TensorFlow Lite y de tipo Cuantificado para ser posible funcionar en un entorno de aplicación móvil.

   NOTA: Teachable Machine sólo es compatible con la arquitectura del modelo
MobileNet a partir de ahora.

1. Asignación de Metadatos.
   
   Se obtiene el archivo generado. Dentro del modelo las clases se agregan junto con los metadatos de todos los modelos de la aplicación de clasificación de imágenes de muestra. Se necesita agregar metadatos al modelo TFLite para adjuntar las clases y demás información necesaria.

   Este procedimiento se realizó dentro de un documento de [Colab](https://colab.research.google.com/).

   ```python
   PASO 1) CREA UNA CARPETA EN GOOGLE DRIVE con metadatos con nombre
   Cree otra carpeta llamada model_with_metadata dentro de la carpeta de metadatos.

   PASO 2) MONTAR LA UNIDAD Y NAVEGAR A LA CARPETA de metadatos

   #mount drive
   %cd ..
   from google.colab import drive
   drive.mount('/content/gdrive')

   # this creates a symbolic link so that now the path /content/gdrive/My\ Drive/ is equal to /mydrive
   !ln -s /content/gdrive/My\ Drive/ /mydrive

   # list the contents of /mydrive
   !ls /mydrive

   #Navigate to /mydrive/metadata
   %cd /mydrive/metadata

   PASO 3) CARGAR LOS SIGUIENTES 3 ARCHIVOS A LA carpeta de metadatos

   1. metadata_writer_for_image_classifier.py
   2. model.tflite & all other models
   3. labels.txt

   PASO 4) INSTALAR EL SOPORTE TFLITE

   pip install tflite-support

   PASO 5) FINALMENTE, SE EJECUTA EL SCRIPT DE PYTHON USANDO EL SIGUIENTE COMANDO
   
   !python metadata_writer_for_image_classifier.py \
    --model_file=/mydrive/metadata/model.tflite \
    --label_file=/mydrive/metadata/labels.txt \
    --export_directory=/mydrive/metadata/model_with_metadata

   El modelo TFLite con metadatos se crea dentro de la carpeta model_with_metadata junto con el archivo .json.

   ```
   Resultado de la asignación de metadatos al modelo:

   <p align="center">
      <img src="/md/tflite_meta.png" data-canonical-src="/md/tflite_meta.png" alt="Metadatos"/>
   </p>

   Fuente: TECHZIZOU
   
   Documento de Colab para más detalles: https://colab.research.google.com/drive/1S9-_AlHOzmvKsmzuGMWOxphnR6F8RxmX?usp=sharing

2.  Integración a proyecto de Android / Kotlin en Android Studio.
    
    Se descarga la aplicación de muestra que proporciona TensorFlow para la clasificación de impagenes, se puede elegir entre la versión de Java o de Kotlin.
    
    Se puede acceder a ambas compilaciones desde el siguiente enlace al repositorio: https://github.com/tensorflow/examples/tree/master/lite/examples/image_classification

    Se procedió a copiar el modelo de TFLite generado con metadatos dentro de la carpeta de assets del proyecto.
    
    La ruta es la siguiente:
    
    *(nombre_proyecto)\app\src\main\assets*

    <p align="center">
      <img src="/md/proyecto_modelo.png" data-canonical-src="/md/proyecto_modelo.png" alt="Modelo"/>
    </p>

    <br>

    Modelo en el proyecto de Android:

    <p align="center">
      <img src="/md/android_modelo.png" data-canonical-src="/md/android_modelo.png" alt="Modelo en el proyecto"/>
    </p>

    <p align="center">
      <img src="/md/android_adap_modelo.png" data-canonical-src="/md/android_adap_modelo.png" alt="Modelo en el proyecto"/>
    </p>
    
    
## Resultados

Pruebas de resultados al utilizar el modelo en el dispositivo móvil real.

Se muestran 3 resultados:

<p align="center">
   <img src="/md/r_cap1.jpg" data-canonical-src="/md/r_cap1.jpg" alt="Resultado" width="250" height="500"/>
</p>

Resultado: 1ra Flor, Vinca, nivel de confianza de 99%.

Se observa la aplicación escaneando la flor y el nivel de confianza y la clase a la que pertenece la flor, en este caso corresponde a una flor de Madagascar periwinkle o en resumen a una vinca.

<hr>

<p align="center">
   <img src="/md/r_cap2.jpg" data-canonical-src="/md/r_cap2.jpg" alt="Resultado" width="250" height="500"/>
</p>

Resultado: 2da Flor, Laurel, nivel de confianza de 100%.

Se observa la aplicación escaneando la flor y el nivel de confianza y la clase a la que pertenece la flor, en este caso corresponde a una flor de Laurel.

<hr>

<p align="center">
   <img src="/md/r_cap3.jpg" data-canonical-src="/md/r_cap3.jpg" alt="Resultado" width="250" height="500"/>
</p>

Resultado: 3ra Flor, Margarita, nivel de confianza de 100%.

Se observa la aplicación escaneando la flor y el nivel de confianza y la clase a la que pertenece la flor, en este caso corresponde a una flor de una Margarita.

---

## Instalación

Nota: La aplicación solo funciona en dispostivos Android.

1. Acceder a https://github.com/AdrianBL1/ClasificadorFlores/releases
2. Descargar el APK de la versión en curso compartida.
3. Instalar el archivo APK descargado.
4. Ejecutar la aplicación.


## Uso

1. Abrir la aplicación instalada.
2. Otorgar permisos de uso de la cámara del dispositivo.
3. Desplegar las opciones de la aplicación.
4. En caso de que no se encuentre seleccionado el modelo "Clasificador de Flores", seleccionarlo en "ML Model" de las opciones de la aplicación.

## Opciones de la aplicación y configuración del modelo

Al tener instalado el modelo en la aplicación, es posible ajustar los parámetros del modelo y de ser posible si se tienen más modelos instalados en el dispositivo hacer la seleccion del modelo para realizar el cambio de ellos.

Se detallan las características de la aplicación.

<p align="center">
   <img src="/md/app_caracteristicas.PNG" data-canonical-src="/md/app_caracteristicas.PNG" alt="Ajuste"/>
</p>

---

Referencias

* Teachable Machine. https://teachablemachine.withgoogle.com/
* Build a custom Image classification Android app using Teachable Machine (Latest Version TensorFlow App). https://techzizou.com/build-a-custom-image-classification-android-app-using-teachable-machine-latest-version-tensorflow-app/