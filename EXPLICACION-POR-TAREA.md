# Explicacion por Tarea: Que se hizo y como se aplico

## Proyecto: La 5ta Esencia - Blog con Bootstrap

---

## Tarea 1: Instalar Bootstrap con un enlace CDN

### Que se hizo
Se instalo Bootstrap 5.3.3 en las 3 paginas del sitio web (index.html, about.html, contact.html) usando enlaces CDN. Se coloco el CSS en el `<head>` y el JavaScript Bundle antes del cierre de `</body>`.

### Como se aplico

**Ejemplo 1 - CSS en el head:**
```html
<head>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
```
Se coloca en el `<head>` para que los estilos se carguen antes de que el navegador muestre el contenido. Si lo pones despues, la pagina se veria sin estilos por un momento.

**Ejemplo 2 - JS Bundle antes de cerrar body:**
```html
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
</body>
```
Se coloca al final del body para no bloquear la carga del HTML. El "bundle" incluye Popper.js que es necesario para que funcione el navbar responsive y las alertas.

**Ejemplo 3 - CSS personalizado despues de Bootstrap:**
```html
<head>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <link href="style.css" rel="stylesheet" type="text/css" />
</head>
```
Nuestro style.css va despues de Bootstrap para que si necesitamos cambiar algo, nuestros estilos tengan prioridad sobre los de Bootstrap.

---

## Tarea 2: Elegir los colores del sitio web

### Que se hizo
Se eligio una paleta de 5 colores usando los colores predefinidos de Bootstrap. Se documentaron en el archivo style.css y se aplicaron de forma coherente en las 3 paginas.

### Como se aplico

**Ejemplo 1 - Dark para navbar y footer:**
```html
<nav class="navbar navbar-dark bg-dark">
```
```html
<footer class="bg-dark text-light">
```
El color Dark (#212529) se usa como fondo del navbar y footer en las 3 paginas, creando un marco visual oscuro que contrasta con el contenido blanco del centro.

**Ejemplo 2 - Warning/Gold para acentos y marca:**
```html
<a class="navbar-brand text-warning">La 5ta Esencia</a>
```
```html
<div class="card border-warning">
```
```html
<h5 class="text-warning">Equipo - La 5ta Esencia</h5>
```
El color Warning (#ffc107, dorado) se usa para el logo, los bordes de las cards de articulos, y los titulos del footer. Da un toque elegante que va con la tematica gourmet.

**Ejemplo 3 - Danger/Red para el link activo:**
```html
<!-- En index.html, Home esta en rojo -->
<a class="nav-link active text-danger fw-bold" href="index.html">Home</a>

<!-- En about.html, About Us esta en rojo -->
<a class="nav-link active text-danger fw-bold" href="about.html">About Us</a>

<!-- En contact.html, Contact Us esta en rojo -->
<a class="nav-link active text-danger fw-bold" href="contact.html">Contact Us</a>
```
El color Danger (#dc3545, rojo) marca la pagina activa en el navbar, tal como muestra el wireframe de Figma.

---

## Tarea 3: Refactorizar el sitio web con Bootstrap

### Que se hizo
Se reemplazo todo el HTML basico original ("Hello world") con componentes de Bootstrap: navbar responsive, grid system de 3 columnas, tipografia con clases utilitarias, y colores de Bootstrap en lugar de CSS manual.

### Como se aplico

**Ejemplo 1 - Navbar refactorizado con Bootstrap:**
```html
<!-- ANTES (HTML basico): -->
<ul>
  <li><a href="index.html">Home</a></li>
  <li><a href="about.html">About Us</a></li>
</ul>

<!-- DESPUES (Bootstrap Navbar): -->
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">
    <a class="navbar-brand fw-bold text-warning" href="index.html">La 5ta Esencia</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse justify-content-center" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link active text-danger fw-bold" href="index.html">Home</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```
El navbar de Bootstrap agrega automaticamente: fondo oscuro, texto claro, boton hamburguesa en movil, animacion de colapso, y posicionamiento responsive. Todo con solo agregar clases.

**Ejemplo 2 - Grid system refactorizado:**
```html
<!-- ANTES (sin grid): -->
<div>Contenido aqui...</div>

<!-- DESPUES (Bootstrap Grid de 3 columnas): -->
<div class="container-fluid">
  <div class="row">
    <div class="col-lg-2 bg-light">AD</div>
    <div class="col-lg-8">Contenido principal</div>
    <div class="col-lg-2 bg-light">News</div>
  </div>
</div>
```
Bootstrap divide la pantalla en 12 columnas. Usamos col-lg-2 (2/12) para AD, col-lg-8 (8/12) para el contenido, y col-lg-2 (2/12) para News. El prefijo "lg" hace que en pantallas chicas las columnas se apilen verticalmente.

**Ejemplo 3 - Tipografia refactorizada:**
```html
<!-- ANTES (HTML basico): -->
<h1>Bienvenidos</h1>
<p>Descripcion del blog</p>

<!-- DESPUES (Bootstrap tipografia): -->
<h1 class="display-4 text-center text-dark mb-4">Bienvenidos a La 5ta Esencia</h1>
<p class="lead text-center text-secondary mb-5">
  El blog donde exploramos el arte de las tablas de quesos gourmet.
</p>
```
`display-4` hace el titulo mas grande y elegante. `lead` destaca el parrafo. `text-center` centra el texto. `text-dark` y `text-secondary` aplican colores. `mb-4` y `mb-5` agregan espacio abajo.

---

## Tarea 4: La pagina de inicio (Home)

### Que se hizo
Se creo la pagina index.html siguiendo el wireframe: un navbar con 3 links, un layout de 3 columnas (AD | Content | News), contenido con 3 articulos de blog, una imagen, un video de YouTube, y un footer con los nombres del equipo.

### Como se aplico

**Ejemplo 1 - Articulos del blog usando Cards de Bootstrap:**
```html
<article class="mb-5">
  <div class="card border-warning">
    <div class="card-body">
      <h2 class="card-title text-dark">El Arte de Armar una Tabla de Quesos Perfecta</h2>
      <p class="card-text text-secondary small">Publicado el 15 de marzo, 2026</p>
      <p class="card-text">Crear una tabla de quesos no es solo colocar ingredientes al azar...</p>
      <img src="https://images.unsplash.com/photo-1452195100486-9cc805987862?w=800&h=400&fit=crop"
        class="img-fluid rounded my-3" alt="Tabla de quesos gourmet">
    </div>
  </div>
</article>
```
Cada articulo es una `card` de Bootstrap con `border-warning` (borde dorado). La clase `img-fluid` hace que la imagen sea responsive y se adapte al ancho disponible. `rounded` le da esquinas redondeadas.

**Ejemplo 2 - Video responsive con Bootstrap:**
```html
<div class="ratio ratio-16x9">
  <iframe src="https://www.youtube.com/embed/dQw4w9WgXcQ"
    title="Video sobre tablas de quesos" allowfullscreen></iframe>
</div>
```
La clase `ratio ratio-16x9` de Bootstrap crea un contenedor que mantiene la proporcion 16:9 sin importar el tamano de la pantalla. El iframe se adapta automaticamente.

**Ejemplo 3 - Footer con grid de 2 columnas:**
```html
<footer class="bg-dark text-light py-4 mt-3">
  <div class="container">
    <div class="row">
      <div class="col-md-6">
        <h5 class="text-warning">Equipo - La 5ta Esencia</h5>
        <ul class="list-unstyled small">
          <li>Fernando - fernando@5taesencia.com</li>
          <li>Daniel - daniel@5taesencia.com</li>
        </ul>
      </div>
      <div class="col-md-6">
        <ul class="list-unstyled small">
          <li>Victor - victor@5taesencia.com</li>
          <li>Eduardo - eduardo@5taesencia.com</li>
        </ul>
      </div>
    </div>
  </div>
</footer>
```
El footer usa `bg-dark text-light` para el fondo oscuro con texto claro. Dentro tiene un `row` con dos `col-md-6` (cada una ocupa la mitad) para distribuir los 10 nombres del equipo en dos columnas. `list-unstyled` quita los puntos de la lista.

---

## Tarea 5: La pagina About Us

### Que se hizo
Se creo about.html con la misma estructura del wireframe (navbar + 3 columnas + footer). El contenido central explica por que existe el proyecto, los valores del equipo, y presenta a los 10 miembros. El link activo del navbar cambia a "About Us" en rojo.

### Como se aplico

**Ejemplo 1 - Seccion "Por que existe el proyecto":**
```html
<section class="mb-5">
  <div class="card border-warning">
    <div class="card-body">
      <h2 class="card-title text-dark">Por que existe La 5ta Esencia?</h2>
      <p class="card-text">
        La 5ta Esencia nacio de una idea simple pero poderosa: llevar la experiencia
        de las tablas de quesos gourmet directamente a tu hogar...
      </p>
      <p class="card-text">
        Nuestro proyecto comenzo como una iniciativa estudiantil y se convirtio en
        algo mas grande: un servicio de delivery...
      </p>
      <img src="https://images.unsplash.com/photo-1556761175-5973dc0f32e7?w=800&h=400&fit=crop"
        class="img-fluid rounded my-3" alt="Equipo de trabajo colaborando">
    </div>
  </div>
</section>
```
Se usa una card de Bootstrap para enmarcar la explicacion del proyecto con borde dorado. Incluye texto descriptivo e imagen del equipo.

**Ejemplo 2 - Valores del equipo con list-group:**
```html
<ul class="list-group list-group-flush">
  <li class="list-group-item">
    <strong class="text-warning">Calidad</strong> - Seleccionamos los mejores productos frescos.
  </li>
  <li class="list-group-item">
    <strong class="text-warning">Artesania</strong> - Cada tabla es ensamblada a mano.
  </li>
  <li class="list-group-item">
    <strong class="text-warning">Puntualidad</strong> - Entregamos a tiempo.
  </li>
</ul>
```
Se usa el componente `list-group` de Bootstrap con `list-group-flush` (sin bordes laterales). Cada valor tiene su nombre en `text-warning` (dorado) para mantener la paleta de colores.

**Ejemplo 3 - Equipo en grid de 2 columnas dentro de una card:**
```html
<div class="card border-warning">
  <div class="card-body">
    <h2 class="card-title text-dark mb-3">Nuestro Equipo</h2>
    <div class="row">
      <div class="col-md-6">
        <ul class="list-group list-group-flush">
          <li class="list-group-item">Fernando - Fundador</li>
          <li class="list-group-item">Daniel - Desarrollo</li>
          <li class="list-group-item">Vianey - Diseno</li>
        </ul>
      </div>
      <div class="col-md-6">
        <ul class="list-group list-group-flush">
          <li class="list-group-item">Victor - Operaciones</li>
          <li class="list-group-item">Eduardo - Finanzas</li>
          <li class="list-group-item">Angel - Contenido</li>
        </ul>
      </div>
    </div>
  </div>
</div>
```
Se anida un grid (`row` + `col-md-6`) dentro de una card para presentar a los miembros del equipo en dos columnas. Esto muestra que el grid de Bootstrap se puede usar en cualquier nivel, no solo para el layout principal.

---

## Tarea 6: La pagina Contact Us

### Que se hizo
Se creo contact.html con un formulario de Bootstrap que tiene campos de email y textarea, un boton de envio, y una alerta live que aparece al hacer clic diciendo "Message sent!" con un boton de dismiss (X) para cerrarla.

### Como se aplico

**Ejemplo 1 - Formulario con componentes Form de Bootstrap:**
```html
<form id="contactForm">
  <div class="mb-3">
    <label for="emailInput" class="form-label fw-bold">Correo Electronico</label>
    <input type="email" class="form-control" id="emailInput"
      placeholder="tucorreo@ejemplo.com" required>
    <div class="form-text">Nunca compartiremos tu correo con nadie.</div>
  </div>

  <div class="mb-3">
    <label for="messageTextarea" class="form-label fw-bold">Mensaje</label>
    <textarea class="form-control" id="messageTextarea" rows="5"
      placeholder="Escribe tu mensaje aqui..." required></textarea>
  </div>

  <button type="submit" class="btn btn-warning fw-bold">Enviar Mensaje</button>
</form>
```
Se usa `form-control` para estilizar los inputs y textarea con los estilos de Bootstrap (bordes redondeados, foco azul). `form-label` estiliza las etiquetas. `form-text` agrega texto de ayuda. El boton usa `btn btn-warning` para el color dorado de la paleta.

**Ejemplo 2 - Alerta live con JavaScript:**
```javascript
const alertPlaceholder = document.getElementById('liveAlertPlaceholder');

function showAlert(message, type) {
  const wrapper = document.createElement('div');
  wrapper.innerHTML = [
    '<div class="alert alert-' + type + ' alert-dismissible fade show" role="alert">',
    '   <strong>' + message + '</strong>',
    '   <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>',
    '</div>'
  ].join('');
  alertPlaceholder.append(wrapper);
}
```
La funcion crea dinamicamente un `<div>` con las clases de alerta de Bootstrap: `alert-success` (verde), `alert-dismissible` (permite cerrar), `fade show` (animacion). El `btn-close` con `data-bs-dismiss="alert"` es el boton X que Bootstrap maneja automaticamente.

**Ejemplo 3 - Conexion del boton con la alerta:**
```javascript
document.getElementById('contactForm').addEventListener('submit', function(event) {
  event.preventDefault();
  showAlert('Message sent! Tu mensaje ha sido enviado exitosamente.', 'success');
  this.reset();
});
```
Cuando el usuario hace clic en "Enviar Mensaje":
1. `event.preventDefault()` evita que la pagina se recargue
2. `showAlert(...)` crea y muestra la alerta verde arriba del formulario
3. `this.reset()` limpia todos los campos del formulario
4. El usuario puede cerrar la alerta haciendo clic en la X (dismiss)

---

## Tarea 7: Pulir el sitio web

### Que se hizo
Se verifico que las 3 paginas funcionaran correctamente: navegacion entre paginas, formulario operativo, alerta con dismiss, layout responsive, footer visible, imagenes cargando, video funcional, y colores coherentes.

### Como se aplico

**Ejemplo 1 - Footer siempre abajo con CSS Flexbox:**
```css
body {
  min-height: 100%;
  display: flex;
  flex-direction: column;
}

.container-fluid.mt-3 {
  flex: 1;
}
```
Sin esto, en paginas con poco contenido el footer quedaria flotando a mitad de pantalla. Con `flex: 1` el contenido principal se estira para empujar el footer hasta abajo.

**Ejemplo 2 - Navegacion consistente entre paginas:**
```
index.html   → Home (rojo)    | About Us (blanco) | Contact Us (blanco)
about.html   → Home (blanco)  | About Us (rojo)   | Contact Us (blanco)
contact.html → Home (blanco)  | About Us (blanco)  | Contact Us (rojo)
```
Cada pagina tiene exactamente el mismo navbar, pero el link activo cambia con `text-danger fw-bold`. Esto permite al usuario saber siempre en que pagina esta.

**Ejemplo 3 - Un solo archivo CSS para todas las paginas:**
```html
<!-- En index.html, about.html y contact.html: -->
<link href="style.css" rel="stylesheet" type="text/css" />
```
Las 3 paginas comparten el mismo `style.css`. Esto cumple con la regla de "1 sola hoja de estilos" y garantiza que cualquier cambio de estilo se aplique en todo el sitio a la vez.

---

## Resumen de componentes Bootstrap utilizados por tarea

| Tarea | Componentes de Bootstrap |
|-------|--------------------------|
| 1     | CDN CSS + JS Bundle |
| 2     | bg-dark, text-warning, text-danger, bg-light, text-light |
| 3     | Navbar, Grid (row/col), Typography (display, lead, fw-bold) |
| 4     | Cards, img-fluid, ratio (video), list-group, list-unstyled |
| 5     | Cards, list-group, list-group-flush, Grid anidado (col-md-6) |
| 6     | Forms (form-control, form-label), Buttons (btn), Alerts (alert-dismissible) |
| 7     | CSS Flexbox personalizado + verificacion de todos los componentes |
