---
marp: true
paginate: true
backgroundColor: white
backgroundImage: url('assets/logo_fomento.png')
backgroundPosition: 75%
backgroundSize: fit
header: "**Diseño de Interfaces Web 2021-2022**"
---

# **CSS Avanzado**

---

## **Contenidos**

- @Media Queries
- Flexbox
- CSS Grid

---

## **@Media Queries**

Son una forma de escribir CSS condicional, es decir, CSS que el navegador solo renderiza si se cumplen ciertas condiciones.

Se emplea fundamentalmente en diseño responsivo para modificar la apariencia de ciertos elementos en función del tamaño de pantalla del dispositivo.

---

Forman parte de las [At-Rules](https://developer.mozilla.org/en-US/docs/Web/CSS/At-rule) de CSS que permiten especificar:

- Metadatos ([@charset](https://developer.mozilla.org/en-US/docs/Web/CSS/@charset) e [@import](https://developer.mozilla.org/en-US/docs/Web/CSS/@import))
  
-  Información condicional ([@media](https://developer.mozilla.org/en-US/docs/Web/CSS/@media) y [@document](https://developer.mozilla.org/en-US/docs/Web/CSS/@document) [*deprecated*])

- Información descriptiva ([@font-face](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face))

---

## ¿Pero... cómo se declaran?

```css
@media [only | not] [media-type] ([media-feature]) {
	// CSS
}
```

---

- **media-type** (opcional): describe la categoría general de un dispositivo:
  - *all* (tipo por defecto) para todos los dispositivos
  - *print* para material impreso y modo *vista de impresión*
  - *screen* para pantallas
  - *speech* para sintetizadores del habla

El operador **only** sirve para ocultar los estilos en navegadores antiguos.

---

- **media-feature**: especifica la propiedad del dispositivo que sirve de punto de corte o referencia para la aplicación del estilo.
  - Aceptan en su mayoría los prefijos *min-* y *max-*
  - Se pueden combinar empleando operadores lógicos como ***and***, o listas separadas por comas (**or**)

En el siguiente enlace podemos encontrar una lista con todas las [***media-features***](https://developer.mozilla.org/es/docs/Web/CSS/@media) soportadas.

---

## ¿Algún ejemplo?

Si el ancho de pantalla es ***mayor o igual a 600px***, establece el *background-color lightblue* a los elementos `<div>`

```css
div {
    background-color: lightgreen;
}


@media only screen and (min-width: 600px) {
  div {
    background-color: lightblue;
  }
}
```

---

Si el ancho de pantalla es **menor o igual a 700px** y está **orientada horizontalmente**, aplica un *background-color lightblue* a los elementos `<div>`

```css
div {
    background-color: lightgreen;
}

@media (max-width: 700px) and (orientation: landscape) { 
  div {
    background-color: lightblue;
  }
}
```

---

Si el ancho de pantalla **NO** es **menor o igual a 700px** (es **mayor a 700px**), aplica un *background-color lightblue* a los elementos `<div>`

```css
div {
    background-color: lightgreen;
}

@media not (max-width: 700px) { 
  div {
    background-color: lightblue;
  }
}
```

---
## **Flexbox**

*Flexbox* es un modulo que intenta proporcionar una manera más efectiva de diseñar, alinear y distribuir el espacio entre objetos en un contenedor, incluso cuando su tamaño es desconocido y/o dinámico.

La idea principal es proporcionar al contenedor la capacidad de alterar las dimensiones de sus objetos para ajustarse de forma óptima al espacio disponible.

---

# Conceptos básicos 

Las propiedades del módulo *Flexbox* se aplican

- Al elemento contenedor o *flex container*
- A los elementos hijos o *flex items*

Hasta ahora, el flujo de diseño por defecto se basaba en el tipo de los elementos HTML que pueden ser de bloque (p. ej. `<div>`) o en linea (p. ej. `<span>`). 

El diseño *flex* se articula en los elementos y dimensiones que se muestran en la figura siguiente.

---

![flex-layout](assets/flex_layout.svg "Elementos del diseño flexible")

---

Propiedades del ***main axis***:

- ***main axis*** - El eje principal de un *flex container* en torno al cual se disponen los *flex items*. No tiene porque ser horizontal (depende de la propiedad *flex-direction*)

- ***main start*** y *main-end* - Los *flex items* se disponen dentro del *flex container* empezando en *main start* y terminando en *main end*

- ***main size*** - La dimension de un *flex item* en el sentido del *main axis*. Puede ser su altura o su anchura.

---

Propiedades del ***cross axis***:

- ***cross axis*** - Eje perpendicular al *main axis*. Su dirección depende del anterior.

- ***cross start*** y ***cross end*** - Los *flex items* se colocan en el *flex container* en la dirección del *cross axix* comenzando en *cross start* y terminando en *cross end*
  
- ***cross size*** - La dimension de un *flex item* en el sentido del *cross axis*. Puede ser su altura o su anchura.

---

# Propiedades *Flexbox*

---

## Propiedades del padre o *Flex container*

### ***display***

Define un *flex container* (*inline* o *block*), activando el contexto *flex* para todos sus hijos directos.

```css
.container {
    display: flex | inline-flex;
}
```

---

<style scoped>
    img {
        width: 60%;
        display: block;
        margin: 0 auto;
    }
</style>


### ***flex-direction***

Establece el *main axis*, y por tanto la dirección y sentido en la que los *flex items* se dispondrán dentro del *flex container*.

![flex-direction-property](assets/flex-direction.svg "propiedad flex-direction")

---

```css
.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
```
- ***row*** (por defecto) - de izquierda a derecha en ltr; a la inversa en rtl
- ***row-reverse*** - de derecha a izquierda en ltr; a la inversa en rtl
- ***column*** - como *row* pero de arriba a abajo
- ***column-reverse*** - como *row-reverse* pero de abajo a arriba

---

### ***flex-wrap***

<style scoped>
    img {
        width: 60%;
        display: block;
        margin: 0 auto;
    }
</style>

Por defecto los *flex items* intentarán colocarse en una sola linea. Este comportamiento puede modificarse por emdio de la propiedad *flex-wrap*.

![flex-wrap](assets/flex-wrap.svg "propiedad flex-wrap")

---

```css
.container {
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```
- ***nowrap*** (por defecto) - todos los items se colocarán en una línea
- ***wrap*** - Los *flex items* se dispondrán en varias lineas, de arriba hacia abajo
- ***wrap-reverse*** - Los *flex items* se dispondrán en varias lineas, de abajo hacia arriba

Se pueden encontrar ejemplos de uso de esta propiedad [aquí](https://css-tricks.com/almanac/properties/f/flex-wrap/).

---

### ***flex-flow***

Atajo para *flex-direction* y *flex-wrap*.

```css
.container {
  flex-flow: column wrap;
}
```

Por defecto se establece a ***row nowrap***.

---

### ***justify-content***

<style scoped>
    img {
        width: 25%;
        display: block;
        margin: 0 auto;
    }
</style>

Define la alineación de los elementos a lo largo del *main axis*.

![flex-justify-content](assets/justify-content.svg "propiedad justify-content")

---

```css
.container {
  justify-content: flex-start | flex-end | center | space-between 
  | space-around | space-evenly | start | end 
  | left | right ... + safe | unsafe;
}
```

- ***flex-start*** (por defecto) - Los elementos se agrupan al inicio de la *flex-direction*
- ***flex-end*** - Los elementos se agrupan al final de la *flex-direction*
- ***start*** - Los elementos se agrupan al inicio de la dirección del modo de escritura
- ***end*** - Los elementos se agrupan al final de la dirección del modo de escritura
  
---

- ***center*** - Los elementos se agrupan en el centro.
- ***space-between*** - Los *flex items* se distribuyen regularmente a lo largo de la *flex-direction*
- ***space-around*** - Los *flex items* se distribuyen regularmente a lo largo de la *flex-direction* dejando entre si el mismo espacio libre, salvo el primer y último elemento de la linea donde el espacio entre los mismos y los limites del *flex container* será la mitad que entre elementos
- ***space-evenly***: Los elementos se distribuyende forma que el espacio entre ellos y con los limites del *flex container* sean iguales

Existen problemas de compatibilidad con algunos navegadores para esta propiedad, se puede encontrar información detallada [aquí](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content).

---

<style scoped>
    img {
        width: 25%;
        display: block;
        margin: 0 auto;
    }
</style>

### ***align-items***

Establece como se distribuyen los elementos a lo largo del *cross axis*. Es la versión de ***justify-content*** para el *cross-axis*.

![flex-align-items](assets/align-items.svg "propiedad align-items")

---

```css
.container {
  align-items: stretch | flex-start | flex-end | center 
  | baseline | first baseline | last baseline | start 
  | end | self-start | self-end + ... safe | unsafe;
}
```

- ***stretch*** (por defecto) - Los elementos se estiran para llenar el contenedor (con respecto a *min-width* y *max-width*)
- ***flex-start / start / self-start*** - Los elementos se agrupan al principio del *cross axis*
- ***flex-end / end / self-end*** - Los elementos se agrupan al final del *cross axis*
- ***center*** - Los elementos se disponen en torno al centro del *cross axis*
- ***baseline*** - Los elementos se alinean conforme a su *baseline*

---

<style scoped>
    img {
        width: 25%;
        display: block;
        margin: 0 auto;
    }
</style>

### ***align-content***

Cuando los elementos se disponen en varias lineas, siempre y cuando exista espacio vacio en la dirección del *cross axis*, distribuye los espacios entre las lineas del *main axis*.

![flex-align-content](assets/align-content.svg "propiedad align-content")

---

```css
.container {
  align-content: flex-start | flex-end | center | space-between 
  | space-around | space-evenly | stretch | start 
  | end | baseline | first baseline | last baseline + ... safe | unsafe;
}
```

Los valores que puede tomar esta propiedad son iguales a los de ***justify-content***.

---

<style scoped>
    img {
        width: 30%;
        display: block;
        margin: 0 auto;
    }
</style>

### ***gap, row-gap, column-gap***

Controla el espaciado entre *flex items*. Aplica solo a los espacios entre elementos, no con los limites del *flex container*.

![flex-gap-property](assets/gap-1.svg "propiedades gap" )

---

```css
.container {
  display: flex;
  ...
  gap: 10px;
  gap: 10px 20px; /* row-gap column gap */
  row-gap: 10px;
  column-gap: 20px;
}
```

[Aquí](https://css-tricks.com/almanac/properties/g/gap/) se puede ver un ejemplod el funcionamiento de esta propiedad.

---

## Propiedades de los hijos o *Flex items*

<style scoped>
    img {
        width: 20%;
        display: block;
        margin: 0 auto;
    }
</style>

### ***order***

Por defecto los elementos hijos se ordenan según de declaran en el código. Esto se puede modificar con la propiedad *order*.

![flex-order](assets/order.svg "propiedad order" )

```css
.item {
  order: 5; /* 0 por defecto */
}
```

---

<style scoped>
    img {
        width: 50%;
        display: block;
        margin: 0 auto;
    }
</style>

### ***flex-grow, flex-shrink***

Define la habilidad de un elemento para crecer/contraerse si es necesario. Acepta un valor que sirve como proporcion e indica que cantidad del espacio disponile dentro del flex container ocupara el elemento.

![flex-grow-shrink](assets/flex-grow.svg "propiedad flex-grow flex-shrink" )

---

```css
.item {
  flex-grow: 4; /* por defecto 0 */
  flex-shrink: 3; /* por defecto 0 */
}
```

Si todos los elementos tienen un *flex-grow* de 1, el espacio del *flex container* se distribuirá por igual. Si uno de los elementos tiene un *flex-grow* de 2, entonces tratará de ocupar el **doble*/*mitad* de espacio disponible del padre que los demás.

---

### ***flex-basis***

Determina el tamaño por defecto de un elemento antes de que el espacio restante del padre sea distribuido. Puede ser una dimensión (p. ej. 20%, 5rem, etc) o una *keyword* como ***auto*** que usaría la anchura o altura, dependiendo de la dimensión principal, o ***content*** que emplea el tamaño del contenido del elemento (mal soportado)

```css
.item {
  flex-basis:  | auto; /* por defecto auto */
}
```

Si todos los elementos tienen un *flex-grow* de 1, el espacio del *flex container* se distribuirá por igual. Si uno de los elementos tiene un *flex-grow* de 2, entonces tratará de ocupar el **doble*/*mitad* de espacio disponible del padre que los demás.

---

### ***flex***

Atajo para ***flex-grow***, ***flex-shrink*** y ***flex-basis*** combinados (***flex-shrink*** y ***flex-basis*** son opcionales).

```css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```

Por defecto se establecen a *0 1 auto*.

Es recomendable utilizar este atajo.

---

<style scoped>
    img {
        width: 40%;
        display: block;
        margin: 0 auto;
    }
</style>

### ***align-self***

Permite sobreescribir el alineamiento por defecto o el especificado con ***align-items*** para elementos individuales.

![flex-align-self](assets/align-self.svg "propiedad align-self" )

---

```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

Para una descripción detallada de los valores que puede tomar esta propiedad ver ***align-items***.

*float*, *clear* y *vertical-align* no tienen efecto sobre esta propiedad.

---

## Ejemplos y actividades

### Actividad 1

Supera los 24 niveles del juego [***Flexbox froggy***](https://flexboxfroggy.com/#es).

### Actividad 2

Supera los 12 niveles del juego [***Flexbox defense***](http://www.flexboxdefense.com/).

---

## Enlaces de interés

- [A guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)









