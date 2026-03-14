# Propuestas para el efecto "Corte de Cabello" (Raspar/Scratch)

Para lograr un efecto donde el usuario pueda "cortar el cabello" interactuando con el cursor (simulando una navaja), de forma eficiente y responsiva, existen dos enfoques principales recomendados:

## 1. SVG con Máscaras Interactivos (SVG Masks)
Este enfoque utiliza gráficos vectoriales. Consiste en definir un patrón (la textura del pelo) y aplicarlo a un elemento que cubre toda la sección. Luego, se utiliza una máscara (`<mask>`) de SVG. A medida que el usuario arrastra el cursor, se dibuja un trazado (`<path>`) de color negro dentro de la máscara, lo que oculta el patrón en esas áreas y revela el fondo.

**Ventajas:**
- **Responsividad nativa:** Los SVG se adaptan naturalmente a cualquier tamaño de pantalla sin perder calidad.
- **Fácil implementación:** Controlar las coordenadas del ratón/táctil y agregarlas a un `<path>` es directo.
- Se integra muy bien si la textura del pelo puede definirse mediante patrones SVG o imágenes embebidas.

**Desventajas:**
- Si el usuario interactúa por mucho tiempo generando un trazado extremadamente largo y complejo, el rendimiento de renderizado del SVG podría disminuir.

## 2. HTML5 Canvas con `destination-out`
Este es el método clásico para hacer efectos de tipo "raspadita" (scratchcard). Se dibuja la textura del cabello sobre un `<canvas>`. Al interactuar con el mouse o la pantalla táctil, se dibuja sobre el canvas usando `globalCompositeOperation = 'destination-out'`. Esto "borra" los píxeles del canvas en el trazo, revelando el contenido en HTML debajo del canvas.

**Ventajas:**
- **Máximo rendimiento (Eficiencia):** Es el método más rápido para borrar píxeles dinámicamente, ideal para movimientos rápidos y continuos.
- **Bordes suaves:** Es muy sencillo crear bordes difuminados y simular un corte de navaja realista.

**Desventajas:**
- **Responsividad requiere código extra:** El canvas usa píxeles fijos. Para hacerlo responsivo, es necesario recalcular su tamaño (ej. con `ResizeObserver`) y redibujar o escalar el contenido cuando la ventana cambia de tamaño.

---
**Conclusión:**
Para una implementación rápida, responsiva por defecto y basada en vectores, **SVG Masks** es una excelente opción. Si el rendimiento es crítico o la textura es muy compleja (fotográfica), **HTML5 Canvas** sería la mejor elección (agregando la lógica de resize). En nuestro prototipo, implementaremos **SVG Masks** ya que resuelve el problema original de responsividad de forma limpia y directa.
