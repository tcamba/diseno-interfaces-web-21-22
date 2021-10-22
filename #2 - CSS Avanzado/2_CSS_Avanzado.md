---
marp: true
paginate: true
backgroundColor: white
backgroundImage: url('assets/logo_fomento.png')
backgroundPosition: 75%
backgroundSize: fit
header: "**Diseño de Interfaces Web 2021-2022**"
---

# CSS Avanzado

---

## Contenidos

- _@Media Queries_
- _Flexbox_
- _CSS Grid_

---

## @Media Queries

Son una forma de escribir CSS que el navegador solo renderiza si se cumplen ciertas condiciones.

Se emplea fundamentalmente en diseño responsivo para modificar la apariencia de ciertos elementos en función de propiedades del dispositivo como el tamaño de pantalla y la orientación.

---

Forman parte de las [At-Rules](https://developer.mozilla.org/en-US/docs/Web/CSS/At-rule) de CSS que permiten especificar:

- Metadatos ([@charset](https://developer.mozilla.org/en-US/docs/Web/CSS/@charset), [@import](https://developer.mozilla.org/en-US/docs/Web/CSS/@import) ...)
  
-  Información condicional ([@media](https://developer.mozilla.org/en-US/docs/Web/CSS/@media), [@document](https://developer.mozilla.org/en-US/docs/Web/CSS/@document) [obsoleto] ...)

- Información descriptiva ([@font-face](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face), [@keyframes](https://developer.mozilla.org/en-US/docs/Web/CSS/@keyframes) ...)

---

## ¿Pero... cómo se declaran?

</br>

```css
@media [only|not] [media-type] ([media-feature]) {
	// CSS
}
```

---

### media-type

Establece el tipo de dispositivo al que aplica el estilo.

- ***all*** (_default_) para todos los tipos de dispositivo
- ***print*** para material impreso y modo vista de impresión
- ***screen*** para pantallas
- ***speech*** para sintetizadores del habla

---

### Operadores ***not*** y ***only***

- El operador ***not*** niega o invierte la condición de ***toda*** la _media query_.

- El operador **only** sirve para que los navegadores antiguos que no soportan _media queries_ las ignoren. No tiene efecto en navegadores modernos.

---

### media-feature

Especifica la característica del dispositivo cuyo valor sirve de referencia para la aplicación del estilo.

Admiten en su mayoría los prefijos ***min-*** y ***max-*** para establecer su valor de referencia mínimo o máximo  .

En el siguiente enlace podemos encontrar una lista con todas las [***media-features***](https://developer.mozilla.org/es/docs/Web/CSS/@media) soportadas.

---

### Operadores ***and*** y ***or*** (list separado por comas)

- El operador ***and*** permite encadenar varias _media features_ en una sola _query_ de modo que el estilo se aplicará solo si todas son verdaderas.
- Separando por comas dos o más _media features_ el estilo aplicará si al menos una de ellas es verdadera. 

\* En el caso de una lista separada por comas, el operador ***not*** invierte en exclusiva la condición a la que antecede, no todas las de la lista.

---

## ¿Algún ejemplo?

#### [Ejemplo 1](https://codepen.io/taciocamba/pen/xxLRKOa)

Si el `ancho de pantalla >= 600 px` cambiamos el color de fondo del `<body>`

```css
body {
    background-color: lightgreen;
}


@media only screen and (min-width: 600px) {
  body {
    background-color: lightblue;
  }
}
```

---

#### [Ejemplo 2](https://codepen.io/taciocamba/pen/yLoVBbP)

Si el `ancho de pantalla <= 700px && orientación == horizontal` cambiamos el color de fondo del `<body>`

```css
body {
    background-color: lightgreen;
}

@media (max-width: 700px) and (orientation: landscape) { 
  body {
    background-color: lightblue;
  }
}
```
---

#### [Ejemplo 3](https://codepen.io/taciocamba/pen/BadQBmL)


Si el `ancho de pantalla <= 700px || orientación == horizontal` cambiamos el color de fondo del `<body>`

```css
body {
    background-color: lightgreen;
}

@media (max-width: 700px), (orientation: landscape) { 
  body {
    background-color: lightblue;
  }
}
```

---

#### [Ejemplo 4](https://codepen.io/taciocamba/pen/BadQBmL)

Negando `dispositivo == pantalla && ancho de pantalla <= 600 px` conseguimos que, siempre y cuando no se cumplan a la vez las anteriores condiciones, se cambie el color de fondo del `<body>`

```css
body {
    background-color: lightgreen;
}

@media not screen and (max-width: 600px) { 
  body {
    background-color: lightblue;
  }
}
```

---
## Flexbox

_Flexbox_ es un módulo CSS que trata de proporcionar una forma más efectiva de diseñar, alinear y distribuir el espacio entre los elementos de un contenedor, incluso cuando su tamaño es desconocido y/o dinámico. Para ello, dota al contenedor de la capacidad de alterar las dimensiones de sus elementos hijos de forma que estos se ajusten de forma óptima al espacio disponible.

---

### Conceptos básicos 

Las propiedades del módulo _Flexbox_ se aplican

1. Al elemento contenedor o _flex container_.
2. A los elementos hijos o _flex items_.

El flujo de diseño _flex_ se articula en torno a los elementos y dimensiones que se muestran en la figura de la siguiente diapositiva

---

![flex-layout](assets/flex_layout.svg "Elementos del diseño flexible")

---

#### _Main Axis_

Es el eje principal de un _flex container_, en torno al cual se disponen los _flex items_. No tiene porque ser el eje horizontal (depende de la propiedad _flex-direction_)

- ***main start*** y ***main-end*** - Los *flex items* se disponen dentro del _flex container_ empezando en _main start_ y terminando en _main end_

- ***main size*** - La dimension de un _flex item_ en el sentido del _main axis_. Puede ser su altura o su anchura.

---

#### _Cross Axis_

Es el eje perpendicular al _main axis_, del que depende su dirección.

- ***cross start*** y ***cross end*** - Los _flex items_ se colocan en el _flex container_ en la dirección del _cross axis_ comenzando en _cross start_ y terminando en _cross end_
  
- ***cross size*** - La dimension de un _flex item_ en el sentido del _cross axis_. Puede ser su altura o su anchura.

---

### Propiedades _Flexbox_

---

### Propiedades del padre o _Flex container_

#### ***display***

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


#### ***flex-direction***

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

#### ***flex-wrap***

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

#### ***flex-flow***

Atajo para *flex-direction* y *flex-wrap*.

```css
.container {
  flex-flow: column wrap;
}
```

Por defecto se establece a ***row nowrap***.

---

#### ***justify-content***

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

#### ***align-items***

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

#### ***align-content***

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

#### ***gap, row-gap, column-gap***

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

### Propiedades de los hijos o *Flex items*

<style scoped>
    img {
        width: 20%;
        display: block;
        margin: 0 auto;
    }
</style>

#### ***order***

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

#### ***flex-grow, flex-shrink***

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

#### ***flex-basis***

Determina el tamaño por defecto de un elemento antes de que el espacio restante del padre sea distribuido. Puede ser una dimensión (p. ej. 20%, 5rem, etc) o una *keyword* como ***auto*** que usaría la anchura o altura, dependiendo de la dimensión principal, o ***content*** que emplea el tamaño del contenido del elemento (mal soportado)

```css
.item {
  flex-basis:  | auto; /* por defecto auto */
}
```

Si todos los elementos tienen un *flex-grow* de 1, el espacio del *flex container* se distribuirá por igual. Si uno de los elementos tiene un *flex-grow* de 2, entonces tratará de ocupar el **doble*/*mitad* de espacio disponible del padre que los demás.

---

#### ***flex***

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

#### ***align-self***

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

### Ejemplos y actividades

#### Actividad 1

Supera los 24 niveles del juego [***Flexbox froggy***](https://flexboxfroggy.com/#es).

#### Actividad 2

Supera los 12 niveles del juego [***Flexbox defense***](http://www.flexboxdefense.com/).

---

## Enlaces de interés

- [A guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

---

## CSS Grid

_CSS Grid_ es un sistema de diseño bi-dimensional (A diferencia de _Flexbox_, que es unidimensional) que ha supuesto un punto de inflexión al resolver la mayoría de los problemas en el diseño web hasta el momento. 

Su uso combinado con _Flexbox_, enfocado a casos de uso diferentes, constituye el núcleo fundamental del diseño web moderno.

---

### Conceptos básicos

#### _Grid container_ 

Es el elemento al que se le aplica la propiedad `display: grid`. Es el padre ***directo*** de todos los _grid items_.

#### _Grid Item_

Los hijos ***directos*** del _grid container_.

---

<style scoped>
    img {
        width: 50%;
        display: block;
        margin: 0 auto;
    }
</style>

#### _Grid Line_ 

Son las líneas que constituyen la estructura del grid. Pueden ser verticales (columnas) u horizontales (filas).

![grid-line](assets/terms-grid-line.svg "Grid line vertical")

---

<style scoped>
    img {
        width: 50%;
        display: block;
        margin: 0 auto;
    }
</style>

#### _Grid Track_ 

Representan las filas o columnas del _grid_.

![grid-track](assets/terms-grid-track.svg "Fila del _grid_")

---

<style scoped>
    img {
        width: 50%;
        display: block;
        margin: 0 auto;
    }
</style>

#### _Grid Area_

El espacio total rodeado por 4 _grid lines_, que puede estar compuesto por cualquier numero de _grid cells_.

![grid_area](assets/terms-grid-area.svg "Área del _grid_")

---

<style scoped>
    img {
        width: 50%;
        display: block;
        margin: 0 auto;
    }
</style>

#### _Grid Cell_

El área entre dos _grid lines_ de fila y dos _grid lines_ de columna. Es la unidad basica del _grid_.

![grid_cell](assets/terms-grid-cell.svg "Celda del _grid_")

---

### Propiedades _CSS Grid_

---

### Propiedades del padre o _grid container_

#### ***display***

Define el elemento como _grid container_.

```css
.container {
  display: grid | inline-grid;
}
```

---

#### ***grid-template-columns*** y ***grid-template-rows***

Define las columnas y las filas del _frid_ con una lista de valores separada por espacios. Los valores representan las dimensiones del _grid track_ y los espacios los _grid lines_.

- **track-size** que puede ser una longitud, un porcentaje o una fracción del espacio disponible en el grid (unidad ***fr***).
- **line-name** nombre arbitrario para la _grid line_. 

---

```css
.container {
  grid-template-columns: ...  ...;
  /* p. ej. 
      1fr 1fr
      minmax(10px, 1fr) 3fr
      repeat(5, 1fr)
      50px auto 100px 1fr
  */
  grid-template-rows: ... ...;
  /* p. ej. 
      min-content 1fr min-content
      100px 1fr max-content
  */
}
```

---

<style scoped>
    img {
        width: 40%;
        display: block;
        margin: 0 auto;
    }
</style>

Si no se establece un nombre para la _grid line_ se le asigna automáticamente un número positivo para identificarla. El -1 identifica la última de todas las _grid lines_

![grid_line_no_name](assets/template-columns-rows-01.svg "Grid lines sin nombre establecido")

---

<style scoped>
    img {
        width: 40%;
        display: block;
        margin: 0 auto;
    }
</style>

Estableciendo un nombre identificativo para cada _grid line_.

```css
.container {
  grid-template-columns: [first] 40px [line2] 50px [line3] auto [col4-start] 50px [five] 40px [end];
  grid-template-rows: [row1-start] 25% [row1-end] 100px [third-line] auto [last-line];
}
```

![grid_line_name](assets/template-columns-rows-02.svg "Grid lines con nombre establecido")

---

Una _grid line_ puede tener más de un nombre.

```css
.container {
  grid-template-rows: [row1-start] 25% [row1-end row2-start] 25% [row2-end];
}
```

Y varias _grid lines_ compartir el mismo nombre. En tal caso, pueden ser referencia por este y su índice.

```css
.item {
  grid-column-start: col-start 2;
}
```

---

Si en la definición existen valores repetidos, se puede usar la funcion _repeat()_.

```css
.container {
  grid-template-columns: repeat(3, 20px [col-start]);
}
```

lo que equivale a

```css
.container {
  grid-template-columns: 20px [col-start] 20px [col-start] 20px [col-start];
}
```

---

Finalmente, la unidad ***fr*** permite establecer el _track size_ a una fracción del espacio disponible en el _grid_.

```css
.container {
  grid-template-columns: 1fr 1fr 1fr;
}
```

donde establecemos el ancho de cada elemento a $\frac{1}{3}$ del ancho total del _grid_.

---

#### ***grid-template-areas***

Define una plantilla para el _grid_, referenciando los nombres de las _grid areas_ especificadas con la propiedad ***grid-area***. Repetir el nombre de una _grid area_ provoca que el contenido se expanda a esas celdas. 

- **<grid-area-name>** – el nombre del área especificada con la propiedad ***grid-area***.
- **.** – un punto representa una celda vacia.
- **none** – no se define ninguna _grid area_

```css
.container {
  grid-template-areas: 
    "<grid-area-name> | . | none | ..."
    "...";
}
```
---

```css
.item-a {
  grid-area: header;
  background-color: orange;
}
.item-b {
  grid-area: main;  
  background-color: blue;
}
.item-c {
  grid-area: sidebar;  
  background-color: red;
}
.item-d {
  grid-area: footer;  
  background-color: green;
}

.container {
  display: grid;
  grid-template-columns: 50px 50px 50px 50px;
  grid-template-rows: auto;
  grid-template-areas: 
    "header header header header"
    "main main . sidebar"
    "footer footer footer footer";
}
```
---

<style scoped>
    img {
        width: 40%;
        display: block;
        margin: 0 auto;
    }
</style>

En el [ejemplo anterior](https://codepen.io/taciocamba/pen/vYJypzV) creamos un _grid_ con cuatro columnas de ancho y tres filas de alto. El área del _header_ ocupa toda la fila superior. La fila del medio está compuesta del _main_ una celda vacia y el _sidebar_. La última fila constituye el _footer_.

![grid-example-1](assets/dddgrid-template-areas.svg "Grid ejemplo 1")

---

En la declaración, todas las filas deben tener el mismo número de celdas.

Con esta sintaxis no se establece nombre alguno para las _grid lines_ (lo que se nombra son las áreas) de modo que se nombran automáticamente. Por ejemplo, si el nombre de un área es _foo_, el nombre de la _grid line_ de fila y columna inicial será _foo-start_ y el de las finales  _foo-end_.

---

#### ***grid-template***

Atajo para ***grid-template-rows***, ***grid-template-columns*** y ***grid-template-areas***.

- **none** – establece las tres propiedades a sus valores por defecto.
- **<grid-template-rows>** / **<grid-template-columns>** – establece ***grid-template-columns*** y ***grid-template-rows*** a los valores especificados, respectivamente, y ***grid-template-areas*** a **none**.

```css
.container {
  grid-template: none | <grid-template-rows> / <grid-template-columns>;
}
```

---

#### ***column-gap***, ***row-gap***

Especifica el tamaño de las _grid lines_.

- **<line-size>** – una longitud

```css
.container {
  column-gap: <line-size>;
  row-gap: <line-size>;

}
```
En el siguiente ejemplo se observa como los _gaps_ o espacios solo aplican a las _grid lines_ entre columnas o filas, y no a los bordes del _grid_.

---

<style scoped>
    img {
        width: 25%;
        display: block;
        margin: 0 auto;
    }
</style>

```css
.container {
  grid-template-columns: 100px 50px 100px;
  grid-template-rows: 80px auto 80px; 
  column-gap: 10px;
  row-gap: 15px;
}
```

![grid-example-2](assets/dddgrid-gap.svg "Grid ejemplo 2")

---

#### ***gap***

Atajo para ***row-gap*** y ***column-gap***.

- **<row-gap>** **<column-gap>** – tamaños.

```css
.container {
  gap: <row-gap> <column-gap>;
}
```

Si no se especifica **row-gap** toma el mismo valor que **column-gap**.

---

#### ***justify-items***

Alinea los _grid items_ a lo largo del eje en linea (filas). Aplica a todos los _grid items_ dentro del _grid container_.

- **start** – dispone los elementos en el borde inicial de su celda.
- **end** – dispone los elementos en el borde final de su celda.
- **center** – dispone los elementos en el centro de su celda.
- **stretch** (_default_) – expande los elemento de forma que ocupen todo el ancho de la celda.

```css
.container {
  justify-items: start | end | center | stretch;
}
```

---

#### ***align-items***

Alinea los _grid items_ a lo largo del eje en bloque (columnas). Aplica a todos los _grid items_ dentro del _grid container_.

- **start** – dispone los elementos en el borde inicial de su celda.
- **end** – dispone los elementos en el borde final de su celda.
- **center** – dispone los elementos en el centro de su celda.
- **stretch** (_default_) – expande los elemento de forma que ocupen todo el alto de la celda.

```css
.container {
  align-items: start | end | center | stretch;
}
```

---

#### ***place-items***

Atajo para  ***align-items*** y ***justify-items***.

- **<align-items>** / **<justify-items>** – Si se omite ***justify-items*** toma el mismo valor que ***align-items***.

Todos los navegadores principales soportan esta propiedad excepto _Edge_.

---

#### ***justify-content***

En ocasiones el tamaño total del _grid_ es inferior al del _grid container_. Esto puede ocurrir si todos los _grid items_ estan dimensionados con unidades absolutas (como _px_). En este escenario se puede alinear el _grid_ en el _grid container_ a lo largo del eje en línea (filas).

- **start** – coloca el _grid_ en el borde inicial del _grid container_.
- **end** – coloca el _grid_ en el borde final del _grid container_.
- **center** – dispone el _grid_ en el centro del _grid container_.
- **stretch** – redimensiona el _grid_ para ocupar el ancho total del _grid container_.

---

- **space-around** – coloca espacios iguales entre cada _grid item_ y medio espacio entre los _grid items_ y los bordes del _grid_.
- **space-between** – coloca espacios iguales entre cada _grid item_ y nada con los bordes del _grid_.
- **space-evenly** – coloca espacios iguales entre cada _grid item_y incluyendo con los bordes del _grid_.

```css
.container {
  justify-content: start | end | center | stretch | space-around | space-between | space-evenly;    
}
```

---

#### ***align-content***

Es la versión vertical de ***justify-content***. Permite alinear el _grid_ en el _grid container_ a lo largo del eje en bloque (columnas).

- **start** – coloca el _grid_ en el borde inicial del _grid container_.
- **end** – coloca el _grid_ en el borde final del _grid container_.
- **center** – dispone el _grid_ en el centro del _grid container_.
- **stretch** – redimensiona el _grid_ para ocupar el alto total del _grid container_.

---

- **space-around** – coloca espacios iguales entre cada _grid item_ y medio espacio entre los _grid items_ y los bordes del _grid_.
- **space-between** – coloca espacios iguales entre cada _grid item_ y nada con los bordes del _grid_.
- **space-evenly** – coloca espacios iguales entre cada _grid item_y incluyendo con los bordes del _grid_.

```css
.container {
  align-content: start | end | center | stretch | space-around | space-between | space-evenly;    
}
```
---

#### ***place-content***

Atajo para ***align-content*** y ***justify-content***.

- **<align-content>** / **<justify-content>** – Si se omite **justify-content**, toma el valor de **align-content**.

Esta propiedad no está soportada por _Edge_.

---

#### ***grid-auto-columns*** y ***grid-auto-rows***

Propiedad **avanzada**. Su uso se describe con detalle en el siguiente [enlace](https://css-tricks.com/snippets/css/complete-guide-grid/#grid-auto-columnsgrid-auto-rows)

Especifica el tamaño de cualquier _grid track_ autogenerado (_grid tracks_ implícito). Estos _grid tracks_ implícitos se crean cuando hay más _grid items_ que celdas en el _grid_ o cuando se coloca un _grid item_ fuera del _grid_ explícito ([diferencia entre implícito y explícito](https://css-tricks.com/difference-explicit-implicit-grids/))

---

#### ***grid-auto-flow***

Propiedad **avanzada**. Su uso se describe con detalle en el siguiente [enlace](https://css-tricks.com/snippets/css/complete-guide-grid/#grid-auto-flow)

En caso de tener _grid items_ que no se colocan explícitamente en el _grid_ actúa un algoritmo de auto-posicionamiento. Mediante esta propiedad se puede controlar como funciona este algoritmo.

---

#### ***grid***

Propiedad **avanzada**. Se describe con detalle en el siguiente [enlace](https://css-tricks.com/snippets/css/complete-guide-grid/#grid) (se desaconseja su uso).

Atajo para ***grid-template-rows***, ***grid-template-columns***, ***grid-template-areas***, ***grid-auto-rows***, ***grid-auto-columns*** y ***grid-auto-flow***.

---

### Propiedades de los hijos o _grid items_

#### ***grid-column-start***, ***grid-column-end***, ***grid-row-start*** y ***grid-row-end***

Determina la posición del _grid item_ en el _grid_ haciendo referencia a unas _grid lines_ específicas. **grid-column/row-start/end** marca el inicio/fin de la linea de la fila/columna.

- **<line>** – número o o nombre de la _grid line_.
- **span <number>** – el elemento se expandirá a lo largo del número especificado de _grid tracks_.

---

- **span <name>** – el elemento se expandirá hasta la siguiente linea con el nombre proporcionado.
- **auto** – indica auto-posicionamiento, _span_ automatico o _span_ por defecto de 1.
```css
.item {
  grid-column-start: <number> | <name> | span <number> | span <name> | auto;
  grid-column-end: <number> | <name> | span <number> | span <name> | auto;
  grid-row-start: <number> | <name> | span <number> | span <name> | auto;
  grid-row-end: <number> | <name> | span <number> | span <name> | auto;
}
```

---

<style scoped>
    img {
        width: 35%;
        display: block;
        margin: 0 auto;
    }
</style>

Por ejemplo

```css
.item-a {
  grid-column-start: 2;
  grid-column-end: five;
  grid-row-start: row1-start;
  grid-row-end: 3;
}
```

![grid-ejemplo-3](assets/grid-column-row-start-end-01.svg "Grid ejemplo 3")

---

<style scoped>
    img {
        width: 35%;
        display: block;
        margin: 0 auto;
    }
</style>

Otro ejemplo

```css
.item-b {
  grid-column-start: 1;
  grid-column-end: span col4-start;
  grid-row-start: 2;
  grid-row-end: span 2;
}
```

![grid-ejemplo-4](assets/grid-column-row-start-end-02.svg "Grid ejemplo 4")

---

### ***grid-column*** y ***grid-row***

Atajo para ***grid-column-start***, ***grid-column-end*** y ***grid-row-start***, ***grid-row-end*** respectivamente.

- **<start-line>** / **<end-line>** – aceptan los mismos valores que las propiedades individuales, incluyendo _span_.

```css
.item {
  grid-column: <start-line> / <end-line> | <start-line> / span <value>;
  grid-row: <start-line> / <end-line> | <start-line> / span <value>;
}

```

Si no se declara un fin de linea, el elemento ocupará 1 _track_ por defecto.

---

### ***grid-area***

Nombra un _grid item_ de forma que pueda ser referenciado mediante una plantilla creada con ***grid-template-area***. De forma alternativa esta propiedad puede ser usada como atajo para ***grid-row-start***, ***grid-column-start***, ***grid-row-end*** y ***grid-column-end***.

- **<name>** – nombre arbitrario
- **<row-start>** / **<column-start>** / **<row-end>** / **<column-end>** – números o líneas nombradas.

 ```css
 .item {
  grid-area: <name> | <row-start> / <column-start> / <row-end> / <column-end>;
}
 ```

 ---

### ***justify-self*** y ***align-self***

Alinea un _grid item_ dentro de una celda a lo largo del eje en linea/bloque (fila/columna). Aplica a un elemento dentro de una sola celda.

- **start** – posiciona el elemento al inicio del borde de la celda.
- **end** – posiciona el elemento al final del borde de la celda.
- **center** – posiciona el elemento en el centro de la celda.
- **stretch** (_default_) – dimensiona el elemento para ocupar todo el ancho/alto de la celda.

```css
.item {
  justify-self / align-self: start | end | center | stretch;
}
```

---

### ***place-self***

Atajo para ***align-self*** y ***justify-self***.

- **auto** – Alinea los _items_ con el valor por defecto.
- **<align-self>** / **<justify-self>** – Si se omite ***justify-self** toma el valor de **align-self**.

---

### Actividades

1 - Posiciona las siguientes imágenes en un _grid_ 4x4 que ocupe todo el _viewport_. Cada imagen debe llenar toda su celda. Añade espacios de separación entre las imágenes.
2 - Completa todos los niveles del juego CSS [Grid Garden](https://cssgridgarden.com/)