# Guia Paso a Paso: Refactorizacion del Blog con Bootstrap

## Proyecto: La 5ta Esencia - Blog de Quesos Gourmet

Esta guia explica como se integro Bootstrap en un sitio web desde cero, paso a paso, pensada para estudiantes de bootcamp.

---

## NIVEL 1: Lo Basico - Entender la Estructura

### Que es Bootstrap?

Bootstrap es una libreria de CSS y JavaScript que te da componentes predefinidos (navbar, cards, formularios, grids, alertas, etc.) para que no tengas que escribir todo el CSS desde cero. Solo agregas clases a tu HTML y Bootstrap se encarga del estilo.

### Que es refactorizar?

Refactorizar significa tomar codigo que ya funciona y mejorarlo sin cambiar lo que hace. En este caso, tomamos un HTML basico ("Hello world") y lo transformamos en un sitio completo usando Bootstrap.

### Estructura del proyecto

```
AD-14-1-Blog-Refactor/
├── index.html        ← Pagina principal (Home)
├── about.html        ← Pagina About Us
├── contact.html      ← Pagina Contact Us
├── style.css         ← Estilos personalizados (complementa a Bootstrap)
├── script.js         ← JavaScript personalizado (vacio por ahora)
├── instructions.md   ← Instrucciones del laboratorio
├── README.md         ← Descripcion del repositorio
└── Wireframe-Backup/ ← Imagenes del wireframe de referencia
```

### El wireframe (mapa del diseno)

Antes de escribir codigo, hay que entender el wireframe. Es como el plano de una casa:

```
+--------------------------------------------------+
|            Home | About Us | Contact Us           |  ← Navbar
+------+-------------------------------+------------+
|      |                               |            |
|  AD  |          Content              |   News     |  ← 3 columnas
|      |                               |            |
+------+-------------------------------+------------+
|                  Footer                           |  ← Footer
+--------------------------------------------------+
```

Todas las paginas comparten esta misma estructura.

---

## NIVEL 2: Instalar Bootstrap (Task 1)

### Paso 1: Agregar el CSS de Bootstrap en el `<head>`

Abre tu archivo HTML y dentro de la etiqueta `<head>`, agrega esta linea:

```html
<head>
  <!-- ... otros meta tags ... -->

  <!-- Esto carga los ESTILOS de Bootstrap desde un servidor externo (CDN) -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

  <!-- Tu CSS personalizado va DESPUES de Bootstrap para poder sobreescribirlo -->
  <link href="style.css" rel="stylesheet" type="text/css" />
</head>
```

**Por que el orden importa?** Si pones tu `style.css` antes de Bootstrap, Bootstrap sobreescribira tus estilos. Al ponerlo despues, TU tienes la ultima palabra.

### Paso 2: Agregar el JavaScript de Bootstrap antes de `</body>`

Al final del body, antes de cerrarlo, agrega:

```html
  <!-- Esto carga el JavaScript de Bootstrap (necesario para navbar responsive, alertas, etc.) -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>

  <!-- Tu script personalizado -->
  <script src="script.js"></script>
</body>
```

**Por que al final del body?** Para que el HTML se cargue primero y el usuario vea contenido rapido. El JS puede esperar.

**Que es el "bundle"?** Incluye Popper.js, que Bootstrap necesita para dropdowns, tooltips y otros componentes interactivos.

### Errores comunes en este paso

- **Poner un hash de integridad (integrity) incorrecto**: Si copias el `integrity="sha384-..."` y esta mal, Bootstrap NO cargara. Si no estas seguro, simplemente no pongas el atributo integrity.
- **Olvidar el JS**: El CSS solo da estilos. Sin el JS, la navbar no se colapsa en movil y las alertas no funcionan.

---

## NIVEL 3: Elegir Colores (Task 2)

### La regla de los 5 colores

El proyecto pide usar 5 colores o menos. Bootstrap tiene colores predefinidos que puedes usar con clases:

| Color      | Clase CSS         | Codigo   | Donde lo usamos            |
|------------|-------------------|----------|----------------------------|
| Dark       | `bg-dark`         | #212529  | Navbar y Footer            |
| Warning    | `text-warning`    | #ffc107  | Logo, acentos, bordes      |
| Danger     | `text-danger`     | #dc3545  | Link activo en el navbar   |
| Light      | `bg-light`        | #f8f9fa  | Columnas laterales AD/News |
| White      | (default)         | #ffffff  | Fondo del contenido        |

### Como se aplican los colores?

No escribes CSS. Solo agregas clases al HTML:

```html
<!-- Fondo oscuro + texto claro -->
<nav class="bg-dark text-light">

<!-- Texto dorado/amarillo -->
<a class="text-warning">La 5ta Esencia</a>

<!-- Texto rojo -->
<a class="text-danger">Home</a>

<!-- Fondo gris claro -->
<div class="bg-light">
```

---

## NIVEL 4: El Navbar (Task 3)

### Anatomia del Navbar de Bootstrap

```html
<!-- navbar: componente base -->
<!-- navbar-expand-lg: en pantallas grandes muestra links, en chicas colapsa -->
<!-- navbar-dark: los textos/iconos del navbar seran claros -->
<!-- bg-dark: fondo oscuro -->
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">

    <!-- MARCA/LOGO: aparece siempre -->
    <a class="navbar-brand fw-bold text-warning" href="index.html">La 5ta Esencia</a>

    <!-- BOTON HAMBURGUESA: solo aparece en pantallas pequenas -->
    <!-- data-bs-toggle="collapse" le dice a Bootstrap que este boton colapsa algo -->
    <!-- data-bs-target="#navbarNav" le dice QUE colapsa (el div con id="navbarNav") -->
    <button class="navbar-toggler" type="button"
      data-bs-toggle="collapse"
      data-bs-target="#navbarNav">
      <span class="navbar-toggler-icon"></span>
    </button>

    <!-- LINKS: se colapsan en movil, se muestran en desktop -->
    <div class="collapse navbar-collapse justify-content-center" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link active text-danger fw-bold" href="index.html">Home</a>
        </li>
        <li class="nav-item d-flex align-items-center">
          <span class="text-secondary">|</span>
        </li>
        <li class="nav-item">
          <a class="nav-link text-light" href="about.html">About Us</a>
        </li>
        <li class="nav-item d-flex align-items-center">
          <span class="text-secondary">|</span>
        </li>
        <li class="nav-item">
          <a class="nav-link text-light" href="contact.html">Contact Us</a>
        </li>
      </ul>
    </div>

  </div>
</nav>
```

### Desglose clase por clase

| Clase                    | Que hace                                                   |
|--------------------------|------------------------------------------------------------|
| `navbar`                 | Activa el componente navbar de Bootstrap                   |
| `navbar-expand-lg`       | Colapsa en pantallas menores a 992px                       |
| `navbar-dark`            | Iconos y textos en color claro                             |
| `bg-dark`                | Fondo oscuro (#212529)                                     |
| `container-fluid`        | Contenedor que ocupa el 100% del ancho                     |
| `navbar-brand`           | Estilo especial para el logo/nombre del sitio              |
| `navbar-toggler`         | El boton hamburguesa                                       |
| `collapse navbar-collapse`| El contenido que se colapsa/expande                       |
| `justify-content-center` | Centra los links horizontalmente                           |
| `navbar-nav`             | Lista de navegacion                                        |
| `nav-item`               | Cada elemento de la lista                                  |
| `nav-link`               | Estilo de link de navegacion                               |
| `active`                 | Marca la pagina actual                                     |
| `fw-bold`                | Font weight bold (texto en negritas)                       |
| `d-flex align-items-center` | Flexbox para centrar el separador "|" verticalmente     |

### Como cambia el link activo en cada pagina?

En `index.html`, Home tiene `text-danger fw-bold`:
```html
<a class="nav-link active text-danger fw-bold" href="index.html">Home</a>
<a class="nav-link text-light" href="about.html">About Us</a>
```

En `about.html`, About Us tiene `text-danger fw-bold`:
```html
<a class="nav-link text-light" href="index.html">Home</a>
<a class="nav-link active text-danger fw-bold" href="about.html">About Us</a>
```

En `contact.html`, Contact Us tiene `text-danger fw-bold`:
```html
<a class="nav-link text-light" href="about.html">About Us</a>
<a class="nav-link active text-danger fw-bold" href="contact.html">Contact Us</a>
```

---

## NIVEL 5: El Grid System - Layout de 3 Columnas (Task 3)

### Como funciona el grid de Bootstrap?

Bootstrap divide la pantalla en **12 columnas**. Tu decides cuantas columnas ocupa cada seccion:

```
|  2  |        8         |  2  |   = 12 columnas total
| AD  |     Content      | News|
```

### El codigo

```html
<!-- container-fluid: contenedor al 100% del ancho -->
<div class="container-fluid mt-3">

  <!-- row: crea una fila del grid -->
  <div class="row" style="min-height: 70vh;">

    <!-- col-lg-2: ocupa 2 de 12 columnas en pantallas grandes (lg) -->
    <div class="col-lg-2 bg-light border-end">
      <h5>AD</h5>
      <p>Espacio reservado para anunciantes</p>
    </div>

    <!-- col-lg-8: ocupa 8 de 12 columnas (el contenido principal) -->
    <div class="col-lg-8">
      <!-- Aqui va el contenido de cada pagina -->
    </div>

    <!-- col-lg-2: ocupa 2 de 12 columnas -->
    <div class="col-lg-2 bg-light border-start">
      <h5>News</h5>
      <p>Espacio reservado para noticias</p>
    </div>

  </div>
</div>
```

### Que significan los prefijos (sm, md, lg, xl)?

| Prefijo | Pantalla         | Pixeles  |
|---------|------------------|----------|
| `col-`  | Extra pequena    | < 576px  |
| `col-sm`| Pequena          | >= 576px |
| `col-md`| Mediana          | >= 768px |
| `col-lg`| Grande           | >= 992px |
| `col-xl`| Extra grande     | >= 1200px|

Usamos `col-lg` para que en pantallas chicas las 3 columnas se apilen verticalmente (responsive).

### Clases de utilidad usadas

| Clase        | Que hace                                    |
|--------------|---------------------------------------------|
| `mt-3`       | Margin top nivel 3 (espaciado arriba)       |
| `p-3`        | Padding nivel 3 (espaciado interno)         |
| `p-4`        | Padding nivel 4                             |
| `bg-light`   | Fondo gris claro                            |
| `border-end` | Borde al lado derecho                       |
| `border-start`| Borde al lado izquierdo                    |
| `text-center`| Texto centrado                              |
| `text-muted` | Texto gris/apagado                          |
| `mb-4`       | Margin bottom nivel 4                       |
| `mb-5`       | Margin bottom nivel 5                       |
| `my-4`       | Margin vertical (arriba y abajo) nivel 4    |

---

## NIVEL 6: El Contenido - Cards y Tipografia (Task 4)

### Cards de Bootstrap

Las cards son contenedores con borde, titulo y cuerpo. Las usamos para cada articulo:

```html
<article class="mb-5">
  <!-- border-warning: borde color dorado -->
  <div class="card border-warning">
    <div class="card-body">
      <!-- card-title: titulo de la card -->
      <h2 class="card-title text-dark">Titulo del Articulo</h2>

      <!-- card-text: parrafos dentro de la card -->
      <p class="card-text text-secondary small">Fecha | Autor</p>
      <p class="card-text">Contenido del articulo...</p>

      <!-- img-fluid: imagen responsive que se adapta al ancho -->
      <img src="url-de-imagen" class="img-fluid rounded my-3" alt="Descripcion">
    </div>
  </div>
</article>
```

### Tipografia de Bootstrap

```html
<!-- display-4: titulo grande y elegante (mas grande que h1 normal) -->
<h1 class="display-4">Bienvenidos</h1>

<!-- lead: parrafo destacado, mas grande que un <p> normal -->
<p class="lead">Subtitulo descriptivo</p>

<!-- small: texto mas pequeno -->
<p class="small">Texto secundario</p>

<!-- fw-bold: negritas, fst-italic: cursiva -->
<p class="fw-bold">Negrita</p>
<p class="fst-italic">Cursiva</p>
```

### Listas con Bootstrap (list-group)

```html
<!-- list-group-numbered: lista numerada con estilo Bootstrap -->
<!-- list-group-flush: sin bordes laterales -->
<ol class="list-group list-group-numbered list-group-flush">
  <li class="list-group-item">Primer tip</li>
  <li class="list-group-item">Segundo tip</li>
</ol>
```

### Video responsivo

```html
<!-- ratio ratio-16x9: hace que el iframe mantenga proporcion 16:9 -->
<div class="ratio ratio-16x9">
  <iframe src="https://www.youtube.com/embed/ID_DEL_VIDEO"
    title="Descripcion" allowfullscreen></iframe>
</div>
```

---

## NIVEL 7: El Footer (Todas las paginas)

### Estructura del footer

```html
<!-- bg-dark: fondo oscuro, text-light: texto claro -->
<!-- py-4: padding vertical, mt-3: margin top -->
<footer class="bg-dark text-light py-4 mt-3">
  <div class="container">

    <!-- row con 2 columnas para los nombres del equipo -->
    <div class="row">
      <div class="col-md-6">
        <h5 class="text-warning">Equipo - La 5ta Esencia</h5>
        <!-- list-unstyled: quita los puntos de la lista -->
        <ul class="list-unstyled small">
          <li>Fernando - fernando@5taesencia.com</li>
          <!-- mas miembros... -->
        </ul>
      </div>
      <div class="col-md-6">
        <ul class="list-unstyled small">
          <li>Victor - victor@5taesencia.com</li>
          <!-- mas miembros... -->
        </ul>
      </div>
    </div>

    <!-- Linea de copyright centrada con borde arriba -->
    <div class="text-center mt-3 border-top pt-3">
      <p class="mb-0 small">&copy; 2026 La 5ta Esencia</p>
    </div>

  </div>
</footer>
```

---

## NIVEL 8: About Us - Contenido del Equipo (Task 5)

La pagina About Us sigue la misma estructura (navbar + 3 columnas + footer) pero el contenido central incluye:

1. **Por que existe el proyecto** - card con texto explicativo + imagen
2. **Nuestros valores** - lista con `list-group` donde cada valor tiene un nombre en `text-warning` (dorado)
3. **El equipo** - grid de 2 columnas (`col-md-6`) dentro de una card con los 10 miembros

Lo importante es que el link activo en el navbar cambia a "About Us" en rojo.

---

## NIVEL 9: Contact Us - Formulario y Alertas (Task 6)

### El formulario de Bootstrap

```html
<form id="contactForm">
  <!-- Campo de email -->
  <div class="mb-3">
    <label for="emailInput" class="form-label fw-bold">Correo Electronico</label>
    <input type="email" class="form-control" id="emailInput"
      placeholder="tucorreo@ejemplo.com" required>
    <div class="form-text">Texto de ayuda debajo del campo.</div>
  </div>

  <!-- Campo de texto largo (textarea) -->
  <div class="mb-3">
    <label for="messageTextarea" class="form-label fw-bold">Mensaje</label>
    <textarea class="form-control" id="messageTextarea" rows="5"
      placeholder="Escribe tu mensaje aqui..." required></textarea>
  </div>

  <!-- Boton de envio -->
  <button type="submit" class="btn btn-warning fw-bold">Enviar Mensaje</button>
</form>
```

### Clases del formulario explicadas

| Clase          | Que hace                                        |
|----------------|-------------------------------------------------|
| `form-label`   | Estilo para labels de formulario                |
| `form-control` | Estilo para inputs y textareas (bordes, padding)|
| `form-text`    | Texto de ayuda pequeno debajo del campo         |
| `btn`          | Estilo base de boton Bootstrap                  |
| `btn-warning`  | Boton color dorado/amarillo                     |
| `mb-3`         | Espacio entre cada campo del formulario         |
| `required`     | Atributo HTML que hace el campo obligatorio      |

### La alerta live con dismiss (lo mas avanzado)

Cuando el usuario hace clic en "Enviar Mensaje", aparece una alerta verde que dice "Message sent!" con un boton X para cerrarla.

```html
<!-- Contenedor vacio donde aparecera la alerta -->
<div id="liveAlertPlaceholder"></div>
```

```javascript
// Referencia al contenedor de alertas
const alertPlaceholder = document.getElementById('liveAlertPlaceholder');

// Funcion que crea la alerta dinamicamente
function showAlert(message, type) {
  const wrapper = document.createElement('div');
  wrapper.innerHTML = [
    // alert-success: alerta verde
    // alert-dismissible: permite cerrarla
    // fade show: animacion de aparicion
    '<div class="alert alert-' + type + ' alert-dismissible fade show" role="alert">',
    '   <strong>' + message + '</strong>',
    // btn-close: boton X para cerrar
    // data-bs-dismiss="alert": le dice a Bootstrap que cierre la alerta
    '   <button type="button" class="btn-close" data-bs-dismiss="alert"></button>',
    '</div>'
  ].join('');

  alertPlaceholder.append(wrapper);
}

// Escuchar cuando se envia el formulario
document.getElementById('contactForm').addEventListener('submit', function(event) {
  // Prevenir que la pagina se recargue
  event.preventDefault();

  // Mostrar la alerta (tipo 'success' = verde)
  showAlert('Message sent! Tu mensaje ha sido enviado exitosamente.', 'success');

  // Limpiar el formulario
  this.reset();
});
```

### Como funciona paso a paso?

1. El usuario llena el email y el mensaje
2. Hace clic en "Enviar Mensaje"
3. JavaScript intercepta el envio (`event.preventDefault()`)
4. Crea un nuevo `<div>` con la clase `alert alert-success` de Bootstrap
5. Lo inserta en el `liveAlertPlaceholder`
6. Bootstrap le aplica los estilos verdes y la animacion
7. El boton X (`btn-close`) permite al usuario cerrar la alerta
8. El formulario se limpia con `this.reset()`

---

## NIVEL 10: CSS Personalizado (style.css)

El archivo CSS es minimo porque Bootstrap hace casi todo el trabajo:

```css
/* Paleta de colores documentada como referencia */
/* 1. Dark (#212529) - bg-dark */
/* 2. Warning (#ffc107) - text-warning */
/* 3. Danger (#dc3545) - text-danger */
/* 4. Light (#f8f9fa) - bg-light */
/* 5. White (#ffffff) - fondo */

html {
  height: 100%;
  width: 100%;
}

body {
  min-height: 100%;
  display: flex;
  flex-direction: column;
}

/* Esto hace que el footer siempre quede abajo */
.container-fluid.mt-3 {
  flex: 1;
}
```

**Por que tan poco CSS?** Porque Bootstrap ya maneja colores, tipografia, espaciado, grid, responsive, etc. Solo necesitamos CSS extra para cosas que Bootstrap no cubre (como el sticky footer con flexbox).

---

## NIVEL 11: Publicar en GitHub Pages

### Paso 1: Crear repositorio local

```bash
git init
git add -A
git commit -m "Initial commit: Blog refactored with Bootstrap"
```

### Paso 2: Crear repositorio en GitHub y subir

```bash
gh repo create "Integrando-bootstrap" --public --source=. --push
```

### Paso 3: Activar GitHub Pages

```bash
gh api repos/TU-USUARIO/Integrando-bootstrap/pages -X POST \
  -f "build_type=legacy" -f "source[branch]=master" -f "source[path]=/"
```

### Paso 4: Tu sitio esta en linea

```
https://TU-USUARIO.github.io/Integrando-bootstrap/
```

---

## Resumen: Que componentes de Bootstrap usamos?

| Componente     | Donde se usa                    | Pagina(s)     |
|----------------|---------------------------------|---------------|
| Navbar         | Navegacion superior             | Todas         |
| Grid (row/col) | Layout de 3 columnas            | Todas         |
| Cards          | Articulos del blog              | Home, About   |
| List Group     | Listas de tips, valores, equipo | Home, About   |
| Forms          | Formulario de contacto          | Contact       |
| Alerts         | Mensaje de confirmacion         | Contact       |
| Typography     | Titulos, parrafos, negritas     | Todas         |
| Colors         | bg-dark, text-warning, etc.     | Todas         |
| Spacing        | mt-3, mb-5, p-4, py-4           | Todas         |
| Responsive     | col-lg, navbar-expand-lg        | Todas         |

---

## Checklist Final (Task 7: Pulido)

- [x] Bootstrap CSS y JS cargando correctamente
- [x] 5 colores o menos
- [x] Navbar funcional en las 3 paginas
- [x] Navbar responsive (hamburguesa en movil)
- [x] Link activo cambia de color en cada pagina
- [x] Grid de 3 columnas (AD | Content | News)
- [x] Home: articulos, imagen, video
- [x] About Us: info del equipo y por que existe el proyecto
- [x] Contact Us: formulario con email + textarea + boton
- [x] Alerta live con dismiss al enviar formulario
- [x] Footer con nombres y emails en todas las paginas
- [x] Un solo archivo CSS (style.css) para todas las paginas
- [x] Sigue el wireframe de Figma
- [x] Publicado en GitHub Pages
