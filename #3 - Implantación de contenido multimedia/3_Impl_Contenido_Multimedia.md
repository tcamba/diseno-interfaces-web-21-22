---
marp: true
theme: uncover
paginate: true
backgroundColor: white
backgroundImage: url('assets/logo_fomento.png')
backgroundPosition: 75%
backgroundSize: fit
header: "**Diseño de Interfaces Web 2021-2022**"
---

<style>
   section {
       font-size: 24px;
   }
</style>

# Implantación de contenido multimedia

---

## Contenidos

- Imágenes
- Audio
- Video

---

## Imagenes

Las imágenes representan de media más del 60% de los bytes necesarios par cargar una página web completa :open_mouth:.

En este escenario, integrar imágenes que se adapten a los diferentes tamaños del _viewport_ y _casos de uso_ de forma suave y optimizando tiempos de carga es una habilidad imprescindible para el diseño moderno de páginas web.

---

### Imagenes en HTML5

Si al potente elemento `img`, que descarga, decodifica y renderiza contenido :muscle: :muscle: :muscle: le sumamos que los navegadores modernos soportan prácticamente cualquier formato de imagen, tenemos un _win win_ de manual. 

Pero como dijo alguien alguna vez en un anuncio de ruedas...

> ***La potencia sin control no sirve de nada***

así que por aquí :arrow_down: dejo una lista de consejos _zen_ :pray:

---

####  Usa tamaños relativos para las imagenes


Tienes para elegir (%, vh, vw, em, ex, rem, ch, vmin o vmax... :sweat:) así que déjate de _px_ para todo sino quieres acabar en :crystal_ball: ***_stack overflow_*** :crystal_ball: como este figura, al que la imagen le desborda el contenedor

![w:320](assets/image_overflowing.png "image overflow")

---

pero por si las :fly: :fly: es buena idea :bulb: hacer algo así

```css
img, embed, object, video {
  max-width: 100%;
}
```
para evitar el desborde limitando la anchura máxima que pueden tomar los elementos multimedia.

---

#### Usa las propiedades ***srcset*** y ***sizes*** del _tag_ `img`
  
Así ayudaras al navegador a elegir la mejor imagen para utilizar en función de las condiciones del dispositivo.

\- ¿***srcset***, ***sizes***... ayudar YO al NAVEGADOR y no al revés :astonished:...? no entiendo nada _hulio_ :laughing:
\- Son propiedades de `img` (:muscle: :muscle: :muscle:) para resolver el _art direction problem_...
\- ¿_art direc_... _whaaaat_? 
\- :eye: :arrow_down:

---

##### _Art direction problem_

:wolf: en la pantalla de mi escritorio

![w:720](assets/lobo-en-el-bosque.jpg)

---

En la pantalla de mi _Iphone_... bonitos :evergreen_tree: :evergreen_tree: :evergreen_tree:

![w:320](assets/lobo-en-el-bosque.jpg)

:rocket: Houston, tenemos un _art direction problem_... ¿qué hacemos?

![w:320](assets/lobo-en-el-bosque-cropped.jpg)

---

Menuda estafa 




- Usa el elemento `picture` cuando quieras especificar diferentes imagenes dependiendo de las características del dispositivo.
- 
- If your page only has one or two images and these are not used elsewhere on your site, consider using inline images to reduce file requests.

