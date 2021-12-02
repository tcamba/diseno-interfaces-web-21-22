# Tarea Evaluable 4

## Criterios de evaluación

Los ejercicios propuestos engloban el contenido impartido en las ***sesiones 9, 10 y 11*** (19-11-2021, 26-11-2021) correspondientes a los temas ***Preprocesadores***  y ***Bootstrap***.

La tarea deberá ser entregada antes del día ***14 de diciembre*** a las ***23:59***. Se dispondrá de una prorroga de 3 días durante la que aplicarán las siguientes penalizaciones:

- Entrega el día ***15 de diciembre de 2021*** : -1 punto
- Entrega el día ***16 de diciembre de 2021*** : -2 puntos
- Entrega el día ***17 de diciembre de 2021*** : -3 puntos

Transcurrido el periodo de prorroga arriba expuesto, se puntuará la tarea con un ***0***.

No se aplicarán criterios de carácter estético en la evaluación de los ejercicios.

La tarea se entregará a través de alguno de los siguientes medios:

- Comprimida en un fichero ***.zip*** a través de la tarea creada a tal efecto en Google Classroom.
- Repositorio de código (Github, Bitbucket ...)
- Servicio IDE Online ([Codepen](https://codepen.io/), [JSFiddle](https://jsfiddle.net/) ...)

## Ejercicios

### 1. Preprocesadores (**50%**)

A partir del siguiente HTML

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Sass - Ejercicio 1 - Actividad 4</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="css/style.css">
</head>

<body>
<article>
    <h1>Galería de imágenes</h1>
    <section>
        <img src="https://picsum.photos/id/237/225/225" alt="black dog">
        <img src="https://picsum.photos/id/447/225/225" alt="man before sea">
        <img src="https://picsum.photos/id/169/225/225" alt="dogs">
        <img src="https://picsum.photos/id/493/225/225" alt="strawberries">
        <img src="https://picsum.photos/id/499/225/225" alt="sunset">
        <img src="https://picsum.photos/id/1075/225/225" alt="tower">
    </section>
</article>
</body>

</html>
```

reproduce el diseño del siguiente video [video :link:](assets/ej-1_tarea-4.mp4)

Instrucciones

- Crea 2 *partials*: _mixins.scss and _reboot.scss
- En la hoja de estilos principal *style.scss*, importa los dos *partials*
- _mixins.scss
  - Escribe un mixin ***frame*** con 6 parametros
  - $thickness: grosor del border
  - $style: estilo del borde (*default* = solid)
  - $color-border: color del borde (*default* = #OOO)
  - $color-bg: color del fondo (*default* = #eee)
  - $padding: padding dentro del elemento (*default* = 10px)
  - $radius: redondeo aplicado al elemento (*default* = 15px)
  - y, cuando se haga *hover*: un `box-shadow`, 0.75 opaque black, 5px de grosor a la derecha y abajo, con un *blur**  de 10px
- _reboot.scss
- - Añade un reset universal y algo de *padding* debajo del encabezado principal
  - body:
    - font: Geneva con una fuente secundaria en caso de fallo
    - texto de color negro en un fondo gris (#ccc)
  - article:
    - `max-width` de 800px, centrado
    - fondo blanco (#fff)
    - contenido centrado
  - section
    - Usa *flexbox* para mostrar las imagenes una al aldo de la otra (con espaciado igual enter ellas), y en multiples lineas cuandos sea necesario
    - img (en section)
      - ancho y alto igual a 225px
      - algod e margen abajo
      - Añade algo de diseño usando el mixin *frame*:
        - 1ra imagen: grosor de borde de 3px, sin especificar el resto de los parámetros del *mixin*
        - 2da imagen: grosor de borde de 3px, estilo de borde a puntos, sin especificar el resto de los parámetros del *mixin*
        - 3ra imagen: grosor de borde de 3px, estilo de borde solido, color de borde `mediumseagreen`, sin especificar el resto de los parámetros del *mixin*
        - 4ta imagen: grosor de borde de 6px, estilo de borde solido, color de borde #b8181b, fondo #e7d5c2, 20px de padding y redondeo de 40px
        - 5ta imagen: grosor de borde de 6px, estilo de borde `dashed`, color de borde rgb(109,85,106), fondo `peru` #e7d5c2, 20px padding y redondeo del 50%
        - 6ta imagen: grosor de borde de 6px, fondo #aac5d9, 20px padding y redondeo del 50%, sin especificar el resto de los parámetros del *mixin*

Las imagénes las podéis elegir libremente

### 2. Bootstrap I (**10%**)

Reproduce el diseño del ejercicio 2 de la tarea 2 usando las clases *flex* que ofrece *Bootstrap*.

<p align=center>
    <img src=assets/holy_grail.png alt=sprites width=600/>
</p>

### 2. Bootstrap II (**10%**)

Reproduce el diseño del ejercicio 3 de la tarea 2 usando el grid o layout que ofrece *Bootstrap*.

<p align=center>
    <img src=assets/holy_grail_grid.png alt=sprites width=600/>
</p>

### 2. Web Libre (**30%**)

Refactorizar la web libre de las tareas anteriores incorporando elementos de *SASS* y *Bootstrap*  (no es necesario que incluya las 2). 

Se puntuará la coherencia en el uso de ambas herramientas. Absteneros de retoques superficiales del estilo 

  - Le añado un *bg-primary* a este div por aqui y ...
  - ... y creo un .scss con una variable que guarde la fuente y la aplique y...
  - *p'alante*

Puntualizo esto porque en la tarea 2 se pidió una refactorización y hubo alumnos que se limitaron a hacer cambios de este estilo.