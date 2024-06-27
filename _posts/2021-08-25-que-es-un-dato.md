---
title: "¿Que es un dato?"
last_modified_at: 2021-08-26T21:15-04:00
categories: [Datos]
tags: [Notas, Datos]
toc: true
coments: true
image:
  path: /assets/img/nota-que-es-un-dato-image.jpg
  lqip: /assets/img/nota-que-es-un-dato-image.jpg
  alt: Una pequeña reflexión sobre lo que es un dato.
---

Con este post comienzo una serie de notas que recopilé hace un tiempo cuando estaba participando en un curso de introducción al análisis de datos.  Estas fueron anotaciones rápidas que me ayudaron a entender y desarrollar una intuición respecto a los temas que maneja el mundo de los datos el cual es muy entretenido.  

# ¿Que es un dato?

Según mi experiencia, es una descripción concreta sobre hechos, elementos, sucesos y entidades que permite estudiarlos, analizarlos o conocerlos.

Creo que es importante resaltar que un dato por si mismo no representa información, es el procesamiento o interpretación de esos datos lo que nos proporciona información.

![Procesamiento Datos](https://upload.wikimedia.org/wikipedia/commons/e/e6/ProcesamientoDatos.svg){: .align-center}

# ¿Como entender los datos?

Podemos entender los datos a través de tres formas simples:

1. **Desde el punto de vista de la programación**, en donde nos interesa la estructura especifica de los datos y sus tipos para construir funciones y flujos que obtengan y procesen información.

2. **Desde el punto de vista estadístico**, que nos orienta hacia las leyes que los rigen, entender los procesos que sigue una variable al medir un evento y de esta forma establecer la estrategia analítica que nos permita obtener información de esos datos.

3. **Desde nuestro propio conocimiento**, en base a lo que sabemos buscamos extraer información importante de lo que esperamos medir en nuestras observaciones.  De esta forma generar alternativas que mejoren su desempeño.

Quiero insistir en que estas son notas rápidas y esto es un resumen, asi que pueden existir infinitas formas de ver los datos, yo solo me limito a tres.  Si encuentro mas voy haciendo la actualización.

# Tipos de datos

Básicamente y a grandes rasgos existen dos tipos de datos:

**Numéricos o cuantitativos** que representan mediciones explicitas como la humedad o temperatura.  En este tipo de datos podemos encontrar:
  - **Datos discretos**, que pueden tomar solo ciertos valores , como la cantidad de participantes de una clase o como el numero de veces que se lanzo una moneda antes de que de cara.  Son valores finitos y que pueden contarse.
  - **Datos continuos_**, que pueden tomar cualquier valor dentro de un rango, como la altura de una persona que puede tomar cualquier valor entre 60cm y 200cm.  La cantidad de opciones es infinita por lo que la única forma de agruparlos es en intervalos, por ejemplo entre 60cm y 90cm, o 120cm y 200cm.

**Categóricos o cualitativos** que no representan mediciones explicitas como una pregunta de verdadero o falso o rangos de sueldo en una encuesta.  Estos pueden ser: 
  - **Datos ordinales**, en donde el orden importa pero el intervalo entre ellos carece de significado, como las notas o calificaciones de una prueba, sabemos que la calificación máxima es una A y que B es la siguiente menor, sin embargo, no podemos restar estas calificaciones y obtener algo util.
  - **Datos nominales**, osea, el orden no importa, como una encuesta de respuesta *si/no/indeciso* o con respuestas codificadas: 1: si, 2:no y 3:no me importa.


No esta demás indicar que si quieres colaborar en este documento, no dudes en ponerte en contacto conmigo para que vamos mejorando el contendido. Se agradece si envían correcciones, puestas al día o incluso párrafos enteros. Esto es muy amable de su parte y es la forma correcta de hacer evolucionar esta guía y el código abierto en general.
{: .notice--success}