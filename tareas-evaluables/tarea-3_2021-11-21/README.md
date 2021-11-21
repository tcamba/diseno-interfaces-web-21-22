# Tarea Evaluable 3

## Criterios de evaluación

Los ejercicios propuestos engloban el contenido impartido en las ***sesiones 6, 7 y 8*** (29-10-2021, 05-11-2021 y 12-11-2021) correspondientes al tema ***Implantación de contenido multimedia*** 

La tarea deberá ser entregada antes del día ***28 de noviembre*** a las ***23:59***. Se dispondrá de una prorroga de 3 días durante la que aplicarán las siguientes penalizaciones:

- Entrega el día ***29 de noviembre de 2021*** : -1 punto
- Entrega el día ***30 de noviembre*** : -2 puntos
- Entrega el día ***1 de diciembre*** : -3 puntos

Transcurrido el periodo de prorroga arriba expuesto, se puntuará la tarea con un ***0***.

No se aplicarán criterios de carácter estético en la evaluación de los ejercicios.

La tarea se entregará a través de alguno de los siguientes medios:

- Comprimida en un fichero ***.zip*** a través de la tarea creada a tal efecto en Google Classroom.
- Repositorio de código (Github, Bitbucket ...)
- Servicio IDE Online ([Codepen](https://codepen.io/), [JSFiddle](https://jsfiddle.net/) ...)

## Ejercicios

### 1. Sprites (**35%**)

Reproduce el siguiente diseño:

<p align=center>
    <img src=assets/diseño_sprites.png alt=sprites width=200/>
</p>

No importa que sea vertical, horizontal o diagonal.

- Haz dos versiones, una utilizando una imagen para cada logo y otra combinándolos en un sprite.
- Cuando el usuario haga hover sobre un logo el fondo debe volverse de un color oscuro.

Si queréis utilizar otra temática que no sea la de los navegadores o algún diseño específico tenéis libertad para ello.

### 2. Optimización web. *Blur-Up Technique* (**65%**)

Poned en práctica la idea del *Blur-Up* ideada por los ingenieros de facebook para las imagenes de *cover* de sus usuarios. Os la recuerdo.

- Cargamos una versión muy pequeña de la imagen de alta calidad que queremos cargar.
- La escalamos al tamaño deseado y le aplicamos un desenfoque gaussiano.
- La sustituimos con una transición suave por la versión de alta calidad de la imagen que deseamos mostrar.

Os proporciono un script con comentarios que tendréis que incluir. Para que funciones es necesario que os ciñais a lo siguiente

- La plantilla HTML debe tener la siguiente estructura. Lo importante es que mantenga los nombres de las clases.

```html
<header class="post-header">
  ...
</header>

    ...

```

- La hoja de estilos debe llamarse `style.css` e incluir los siguientes estilos

```css

.post-header {

    ...
  
    background-image: url(data:image/svg+xml;charset=utf-8,AQUI LA IMAGEN MINUSCULA CODIFICADA EN BASE-64);

    transform: translateZ(0);
}

.post-header-enhanced {

    ...

    background-image: url(AQUI LA RUTA A LA IMAGEN DE ALTA CALIDAD);

    animation: sharpen .5s both;
}

@keyframes sharpen {
from {
    background-image: filter(url(AQUI LA RUTA A LA IMAGEN DE ALTA CALIDAD), blur(20px));
}
to {
    background-image: filter(url(AQUI LA RUTA A LA IMAGEN DE ALTA CALIDAD), blur(0px));
}
}
```

y por aqui el *javascript*

```javascript
window.onload = function loadStuff() {
  var win, doc, img, header, enhancedClass;
  // Si es un navegador viejo tipo IE 8, bye bye no tenemos nada que hacer aquí
  if (!('addEventListener' in window)) {
    return;
  }

  win = window;
  doc = win.document;
  img = new Image();
  header = doc.querySelector('.post-header');
  enhancedClass = 'post-header-enhanced'; // Clase HTML que vamos a aplicar cuando se cargue la imagen de alta calidad

  // Buscamos la primera mención de una url para background-image incluso aunque el estilo no se haya aplicado todavía
  var bigSrc = (function() {
    // Busca todas las reglas CSS en la hoja de estilos
    var styles = doc.querySelector('style').sheet.cssRules;
    // Buscamos entre las reglas CSS la declaración de la imagen de fondo background-image
    var bgDecl = (function() {
      // ...usando una funcion en linea con un loop que recorre dichas reglas
      var bgStyle, i, l = styles.length;
      for (i = 0; i < l; i++) {
        // ...y comprueba que se trata de la regla CSS que tiene como objetivo
        // la clase mejorada o enhanced
        if (styles[i].selectorText &&
          styles[i].selectorText == '.' + enhancedClass) {
          // Si coincide, entonces establecemos la variable bgDecl al valor de toda la background-image
          // de esa regla CSS...
          bgStyle = styles[i].style.backgroundImage;
          // ...y rompemos el bucle
          break;
        }
      }
      // ...y devolvemos el texto.
      return bgStyle;
    }());
    // Esto es mas complejo pero básicamente utiliza una expresion regular para "extraer" 
    // la URL de la imagen de fondo de la cadena que acabamos de cargar (si la hemos encontrado vamos...)
    return bgDecl && bgDecl.match(/(?:\(['|"]?)(.*?)(?:['|"]?\))/)[1];
  }());

  // Creamos una función que se ejecutará cuando se cargue la imagen grande
  // y que cambiara la clase post-header por post-header-enhanced quedando asi
  // aplicados los estilos nuevos
  img.onload = function() {
    header.className += ' ' + enhancedClass;
  };
  // Para terminar disparamos todo el proceso asignando al tag img la url del la imagen de alta calidad
  if (bigSrc) {
    img.src = bigSrc;
  }
};
```

Os recomiendo que utilicéis [codepen](https://codepen.io/) para hacer y entregar el ejercicio para evitar problemas de compatibilidad.
Llevad cuidado con el desenfoque gaussiano `filter()`. Apenas tiene soporte en los navegadores. Os dejo [aqui](https://caniuse.com/css-filter-function) una guía de compatibilidad.

Es una actividad relativamente dificil y para ver las transiciones tendréis que recargar la web varias veces o meter mano al *javascript* para introducir tiempos de parada con *sleep()*