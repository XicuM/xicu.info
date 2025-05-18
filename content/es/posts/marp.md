---
title: Cómo programar presentaciones con Marp
date: 2024-11-25T10:35:33+02:00
comments: true
showToc: true
cover:
   image: posts/marp/cover.jpg
---


## ¿Qué es Marp?

Marp es una herramienta para crear presentaciones visualmente atractivas desarrollada por [Yuki Hattori](https://github.com/yhatt). Como característica diferencial, Marp utiliza Markdown, un lenguaje de marcado ligero y de texto plano conocido por ser fácil de leer y escribir.

La sintaxis sencilla de Markdown lo ha hecho popular entre escritores y desarrolladores para producir contenido que sea estructurado y legible. Marp se basa en esta simplicidad, transformando Markdown en diapositivas de aspecto profesional con mínimo esfuerzo.

En Marp, el enfoque se centra en el contenido, escribiéndolo en texto plano con comandos básicos de Markdown, sin la distracción de herramientas de diseño complejas.


## Cómo instalar y usar Marp

Hay varias formas de instalar y usar Marp. La que yo uso es la extensión de Marp para Visual Studio Code. Esta extensión te permite crear, previsualizar y exportar presentaciones de Marp directamente sin salir del editor de VS Code.

Para instalar la extensión de Marp, sigue estos pasos:

1. Abre Visual Studio Code (si no lo tienes instalado, puedes descargarlo desde [aquí](https://code.visualstudio.com/)).
2. Ve a la vista de Extensiones y busca "Marp" en el cuadro de búsqueda de Extensiones.
3. Haz clic en el botón "Instalar" para instalar la extensión.

{{< figure src="https://marp.app/assets/marp-for-vs-code.png" width=575px align=center >}}


## Cuatro simples pasos para crear una presentación con Marp

Comencemos con un ejemplo simple para mostrarte lo fácil que es crear una presentación con Marp, enfocándonos por el momento solo en el contenido.

### 1. Crear el archivo Markdown
Una vez que la extensión esté instalada, puedes comenzar a crear presentaciones de Marp iniciando un nuevo archivo Markdown. Puedes hacerlo creando un nuevo archivo con la extensión `.md`. Si es la primera vez que usas Visual Studio Code, te pedirá que instales las extensiones recomendadas para el resaltado y previsualización de Markdown, para que puedas identificar fácilmente títulos, enlaces y otras características de la sintaxis de Markdown.

### 2. Habilitar Marp y comenzar a escribir
Para habilitar Marp en el archivo Markdown, necesitas agregar `marp: true` al principio del archivo, envuelto en tres guiones. Luego, puedes comenzar a escribir tu presentación usando Markdown. [Esta guía](https://www.markdownguide.org/basic-syntax/) proporciona una explicación detallada de la sintaxis básica. Se podría comenzar, por ejemplo, con el siguiente código:

```markdown
---
marp: true
headingDivider: 1
---

# Diapositiva 1
Ahora puedes comenzar a escribir tu presentación usando Markdown...

# Diapositiva 2
...y crear tantas diapositivas como necesites.
```

Obseva el uso de la directiva headingDivider en el preámbulo, que te permite separar las diapositivas por el número de caracteres `#` en los encabezados. De lo contrario, puedes usar `---` para separar las diapositivas.

### 3. Previsualizar el contenido

Puedes previsualizar lo que estás escribiendo en todo momento. Para hacerlo, simplemente haz clic en el botón `Open Preview` to the Side en la esquina superior derecha del editor.

### 4. Exportar la presentación

Finalmente, para exportar la presentación, haz clic en el botón Show Quick Pick of Marp Commands en la esquina superior derecha del editor y selecciona Export slide deck. Puedes elegir entre varios formatos, como PDF, PNG, PowerPoint o HTML.

## Trabajar con imágenes

Hasta ahora, solo hemos usado texto para crear las diapositivas. Sin embargo, todos sabemos que una imagen vale más que mil palabras. Por lo tanto, aprenderemos ahora cómo agregar imágenes a nuestra presentación, así como cómo personalizarlas según nuestras necesidades.

### Añade una imagen

Para agregar una imagen a una diapositiva, puedes usar la siguiente sintaxis:

```markdown
![Texto alternativo](/ruta/a/la/imagen.jpg) 
```

La ruta a la imagen puede ser una ruta absoluta o una ruta relativa al archivo Markdown. Por otro lado, la etiqueta Texto alternativo es el texto que se mostrará si la imagen no se puede cargar.

Si no quieres escribir rutas, tienes suerte porque Visual Studio Code te permite arrastrar y soltar la imagen en el editor, lo que copiará automáticamente la imagen en tu directorio de trabajo.

Finalmente, también podrías usar una URL a una imagen alojada en internet, como esta:

```markdown
![Texto alternativo](https://example.com/imagen.jpg) 
```

### Modifica la imagen

En Marp, puedes incluir palabras clave en la etiqueta de `Texto alternativo` para modificar la imagen. La lista completa de directivas se puede encontrar [aquí](https://marpit.marp.app/image-syntax). Las directivas más utilizadas son las siguientes:

#### Cambiar el tamaño de la imagen

Con las siguientes palabras clave, puedes cambiar el tamaño de la imagen, especificando el ancho y/o la altura en píxeles. Aquí hay algunos ejemplos:

- Ancho: `![w:250](/ruta/a/la/imagen.jpg)`
- Altura: `![h:120](/ruta/a/la/imagen.jpg)`
- Ancho y altura: `![w:32 h:32](/ruta/a/la/imagen.jpg)`

La relación de aspecto se mantiene si solo se especifica una de las dimensiones.

#### Establecer la imagen como fondo

Para establecer la imagen como fondo de toda la diapositiva, puedes usar la siguiente estructura:

```markdown
![bg](/ruta/a/la/imagen.jpg)
```

Además, puedes redimensionar la imagen con las siguientes palabras clave:

- `bg fit`: Escalar la imagen para que se ajuste a la diapositiva.
- `bg auto`: Usar el tamaño original de la imagen.
- `bg 150%`: Escalar la imagen por el porcentaje especificado.

Por otro lado, puedes crear un fondo dividido con la siguiente sintaxis:

```markdown
![bg left](/ruta/a/la/imagen.jpg)
```

{{< figure src=https://marpit.marp.app/assets/image-syntax/split-background.jpg align=center width=300px >}}

Esto establecerá la imagen como fondo de la mitad izquierda de la diapositiva. También puedes usar `bg right` para establecer la imagen como fondo de la mitad derecha de la diapositiva. Para especificar el tamaño, agrega el porcentaje después de las palabras clave, por ejemplo, `bg right:33%`.

## Personaliza tu presentación con un tema CSS

En las secciones anteriores, los ejemplos se basaron en el tema predeterminado de Marp. Sin embargo, Marp te permite personalizar la apariencia de tu presentación usando temas CSS, de manera similar a como lo harías con un sitio web.

### Usar un tema incorporado

Marp viene con un conjunto de temas incorporados. Para usar uno de estos, necesitas agregar la directiva `theme`, especificando el nombre del tema. Por ejemplo:

```yaml
marp: true
theme: gaia
```

{{< figure src=https://files.speakerdeck.com/presentations/3f84f66126ed45f88640b2e557942c4e/slide_2.jpg align=center width=300px >}}

### Usar un tema externo

Para usar temas externos, debes configurar Visual Studio Code para reconocer los archivos CSS:

1. Ve a la configuración haciendo clic en el icono de engranaje en la esquina inferior izquierda de la ventana.
2. Busca `marp themes` en el cuadro de búsqueda.
3. En la sección `Marp: Themes`, agrega la ruta al archivo CSS que deseas usar. Por ejemplo, si tienes un archivo CSS llamado `style.css` en el mismo directorio que el archivo Markdown, debes agregar `./style.css` para que Visual Studio Code lo reconozca.

Una vez que hayas configurado Visual Studio Code para reconocer el archivo CSS, puedes descargar el archivo CSS de internet. [Aquí](https://rnd195.github.io/marp-community-themes/) tienes una colección de temas creados por la comunidad de Marp.

Luego, debes agregar la directiva `theme` en el preámbulo, seguida del nombre del tema, para activarlo. Puedes encontrar el nombre del tema al inicio del archivo CSS, indicado por la etiqueta `@theme theme-name`.

### Usar mi tema personalizado

#### Descargar y activar el tema
He creado un tema minimalista que puedes usar en tus presentaciones. Puedes descargar el archivo CSS desde aquí y agregar el siguiente preámbulo a tu archivo Markdown:

```yaml
marp: true
theme: minimal
paginate: true
headingDivider: 2
style: |
   h2:before {
      /* Agrega el título de la presentación aquí */
      content: '/ Título / ';
   }
```

Este preámbulo indica que las páginas tienen indicadores de número de página y se crea una diapositiva cada vez que se declara un encabezado H2 (`##`). Además, el título de la presentación se muestra en cada diapositiva.

La explicación de cómo crear un tema personalizado está fuera del alcance de esta publicación, pero puedes encontrar más información al respecto en [este enlace](https://marpit.marp.app/theme-css). Si estás realmente interesado en crear tu propio tema, por favor házmelo saber en los comentarios y escribiré un post al respecto.

#### Añadir un logo

El tema también admite el uso de un logo. Se agrega a la presentación pegando un PNG llamado `logo.png` en el mismo directorio que el archivo Markdown. El logo predeterminado se puede descargar [aquí](/icons/logo-light.png).

El logo se mostrará en la esquina superior izquierda de las diapositivas. Es posible que necesites ajustar la posición del encabezado si la relación de aspecto del logo es diferente a la predeterminada.

#### Clases personalizadas
Además de las clases incorporadas por defecto en Marp, puedes crear clases personalizadas para aplicar a las diapositivas. Si deseas aplicar una clase personalizada globalmente, puedes agregar la directiva `class` en el preámbulo, seguida del nombre de la clase. De lo contrario, puedes agregar la directiva `_class` en la diapositiva a la que deseas aplicar la clase.

En el archivo CSS de mi tema, he definido algunas clases personalizadas para invertir el esquema de colores y crear columnas. Aquí puedes encontrar dos ejemplos:

- Para invertir el esquema de colores, usa la directiva `_class: invert`.
   ```markdown
   ## Diapositiva 1
   <!-- _class: invert -->
   El fondo de esta diapositiva es negro y el texto es blanco.
   ```

- Para crear dos columnas, usa la directiva `_class: col2`. Puedes crear hasta 4 columnas usando `col3` y `col4`. Cada columna está separada por un encabezado H3 (`###`).
   ```markdown
   ## Diapositiva 2
   <!-- _class: col2 -->
   ### Columna 1
   Esta diapositiva...
   ### Columna 2
   ...está dividida en dos columnas.
   ```

#### Ejemplo
A modo de ejemplo, he recreado esta publicación (en inglés) usando mi tema personalizado. Puedes descargar el código fuente accediendo a [este enlace](/post/marp/marp_tutorial.md). El resultado se muestra a continuación:

{{< adobepdf url="/posts/marp/marp_tutorial.pdf" height="480px" name="Tutorial de Marp" >}}

## Conclusión
Si has llegado hasta aquí, estás listo para comenzar a crear presentaciones hermosas con Marp. ¡Disfruta! 🚀