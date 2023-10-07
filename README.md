# Clasificador de Flores
Modelo Clasificador de Flores.

Desarrollo de Modelo y Aplicación móvil en Android (Android y Koltin) implementando un clasificador de flores.

## Objetivo

* Diseño  de una red neuronal que reconozca flores endémicas de una región en concreto.
* Crear el modelo y exportalo para su implementación en una aplicación móvil.

## Desarrollo

Modelo

La plataforma de entrenamiento utilizada para entrenar nuestro clasificador de imágenes personalizado es la máquina de enseñanza con Google, [Teachable Machine](https://teachablemachine.withgoogle.com/). Esta es una
plataforma utilizada para el proceso de entrenamiento de aprendizaje
profundo con solo unos pocos clics. 

Procedimiento

Primero, cargando las diferentes clases de objetos de su sistema o usando una cámara web, luego entrenándolo. Finalmente, después de la capacitación, puede exportar el modelo de su elección. Se puede elegir el formato que desee y descargar el modelo. Se estará entrenando un modelo para la clasificación de
imágenes de máscaras.

![Alt text](https://cdn-images-1.medium.com/max/2000/0*-dV9UFJJLgIadKgH.png "Optional title")

Requerimientos
* El conjunto de datos de imagen de objeto personalizado con diferentes clases.
* Android Studio 3.2 + (instalado en una máquina Linux, Mac o Windows).
* Dispositivo Android en modo desarrollador con depuración USB habilitada.
* Un cable USB (para conectar el dispositivo Android a la computadora).

---

Referencias

* Teachable Machine. https://teachablemachine.withgoogle.com/
* Build a custom Image classification Android app using Teachable Machine (Latest Version TensorFlow App). https://techzizou.com/build-a-custom-image-classification-android-app-using-teachable-machine-latest-version-tensorflow-app/