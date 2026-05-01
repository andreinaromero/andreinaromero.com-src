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
