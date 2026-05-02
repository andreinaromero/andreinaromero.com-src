# Andreina Romero - Baking Lover 🍰

Este blog es un espacio dedicado a compartir el camino en el aprendizaje de la repostería, fusionando el análisis algorítmico (dado el trasfondo en Computación de la autora) con la pasión por la cocina. Se enfoca tanto en repostería tradicional como en opciones más saludables y menos calóricas.

## Rol del Editor (Gemini CLI) 🤖
Como editor de este blog, mi función es:
- Ayudar en la creación y edición de contenidos (posts y recetas).
- Mantener la consistencia en el estilo y tono del blog.
- Gestionar aspectos técnicos del sitio (Hugo, layouts, estilos).
- Implementar y retirar elementos promocionales (como el banner).

## Guía de Desarrollo Local 💻

Para previsualizar el sitio web en tu máquina local, utiliza el siguiente comando:

```bash
hugo server -D
```

- **-D**: Incluye los posts marcados como borradores (drafts).
- El sitio estará disponible por defecto en: `http://localhost:1313/`

## Referencia: Banner de Promoción 🚩
Para volver a activar el banner, sigue estas instrucciones:

### 1. Reinstalar el CSS
Crea el archivo `static/css/banner.css` con el siguiente contenido:

```css
/* Banner styles */
.banner {
  background-color: #D2B48C; /* Light brown - Tan */
  color: #FFFFFF; /* Light letters - White */
  padding: 15px 0;
  overflow: hidden;
  white-space: nowrap;
  box-sizing: border-box;
  width: 100%;
}

.banner-text {
  display: inline-block;
  padding-left: 100%;
  animation: marquee 30s linear infinite;
  font-size: 2.0rem;
  font-weight: bold;
}

/* Marquee animation */
@keyframes marquee {
  0%   { transform: translate(0, 0); }
  100% { transform: translate(-100%, 0); }
}
```

### 2. Vincular el CSS
En `layouts/partials/custom_head.html`, añade la siguiente línea al principio:
```html
<link rel="stylesheet" href='{{ "css/banner.css" | absURL }}'>
```

### 3. Añadir el HTML
En `layouts/_default/baseof.html`, inserta el bloque del banner justo después de la apertura de la etiqueta `<body>`:

```html
    <!-- PROMOTION BANNER START -->
    <div class="banner">
      <p class="banner-text">ESCRIBE AQUÍ EL TEXTO DE LA PROMOCIÓN</p>
    </div>
    <!-- PROMOTION BANNER END -->
```

## Procesamiento de Imágenes 📸

Cuando se añada una nueva receta con una imagen en formato `.HEIC`, el proceso es el siguiente:

1. **Conversión y Redimensión:** Las imágenes deben convertirse a `.jpg` y redimensionarse a un **ancho de 700px** (manteniendo la proporción original).
2. **Nomenclatura:** La imagen debe tener el **mismo nombre** que el archivo markdown de la receta (ej: `galletas_coco.md` -> `galletas_coco.jpg`).
3. **Herramientas:** En entorno macOS (Darwin), se utiliza `sips`:
   ```bash
   sips -s format jpeg -Z 700 imagen_original.HEIC --out static/images/nombre_receta.jpg
   ```
4. **Limpieza:** Una vez generada la versión `.jpg` en `static/images/`, el archivo original `.HEIC` **debe ser eliminado**.
5. **Vinculación Automática:** El editor debe incluir automáticamente el enlace a la imagen al principio del contenido de la receta: `![Título de la Receta](../../images/nombre_receta.jpg)`.

## Proceso para Añadir una Nueva Receta 🍪

Para agregar una nueva receta al blog y actualizar la sección de destacados en la página de inicio, sigue estos pasos:

### 1. Generar el archivo y procesar la imagen
- Crear el archivo markdown con `hugo new recipes/nombre_de_la_receta.md`.
- Si hay imagen, procesarla siguiendo el protocolo de **Procesamiento de Imágenes**.

### 2. Completar la información de la receta
- **Imagen:** Incluir el link `![Título](../../images/nombre.jpg)` justo debajo del frontmatter.
- **Separador:** Añadir una línea separadora `___` después de la imagen.
- **Contenido:** Tabla de ingredientes (en gramos).
- **Video de YouTube (Opcional):** Si la receta tiene un video, añadir una línea separadora `___` después de la tabla de ingredientes, seguida del texto `Puedes ver el procedimiento completo aquí:` y el código de inserción (`iframe`) de YouTube. Cerrar con otra línea separadora `___`.
- **Procedimiento:** Lista numerada de pasos.

## Inserción de Videos de YouTube 📺

Cuando se incluya un video de YouTube en una receta o post, se debe seguir este formato:

1. **Ubicación:** Generalmente después de la tabla de ingredientes y antes del procedimiento detallado.
2. **Separadores:** Enmarcar el bloque del video entre dos líneas separadoras `___`.
3. **Texto Introductorio:** Incluir la frase `Puedes ver el procedimiento completo aquí:` justo antes del `iframe`.
4. **Código Embed:** Utilizar el código estándar de YouTube (ancho 560, alto 315).
5. **Placeholder (Si no hay link):** Si el video aún no está listo, utilizar el siguiente bloque como marcador de posición:
   ```markdown
   ___

   Puedes ver el procedimiento completo aquí: 
   <!-- YOUTUBE_VIDEO_PLACEHOLDER -->
   *(Video en proceso de edición)*

   ___
   ```

Ejemplo:
```markdown
___

Puedes ver el procedimiento completo aquí: 
<iframe width="560" height="315" src="https://www.youtube.com/embed/VIDEO_ID" ...></iframe>

___
```

### 3. Rotación en la Página de Inicio
Las recetas destacadas se gestionan en `content/homepage/recetas.md`. El flujo de rotación es el siguiente:
1. Identifica las 3 recetas actuales.
2. **Elimina la tercera receta** de la lista.
3. Inserta la **nueva receta** en la **primera posición**.
4. Las que eran primera y segunda bajan un puesto cada una.

Ejemplo de estructura en `recetas.md`:
```markdown
{{<icon class="fa fa-hand-o-right">}}&nbsp;[NUEVA RECETA 🍪](recipes/nueva_receta)
{{<icon class="fa fa-hand-o-right">}}&nbsp;[RECETA ANTERIOR #1 🍰](recipes/receta_1)
{{<icon class="fa fa-hand-o-right">}}&nbsp;[RECETA ANTERIOR #2 ☕](recipes/receta_2)
```

