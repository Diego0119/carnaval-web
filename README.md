# Carnaval de Invierno 2025 - Sitio Web

Este proyecto es un sitio web desarrollado con **Astro** como framework principal y **WordPress en modo Headless** como fuente de datos. El sitio promociona el "Carnaval de Invierno 2025" de Punta Arenas, incluyendo votaciones, descuentos y contenido multimedia.

---

## 🛠️ Tecnologías Utilizadas

- **Astro**: Framework estático moderno para el frontend.
- **WordPress Headless**: Usado como CMS para gestionar entradas y contenido, accedido mediante GraphQL.
- **GraphQL**: Consultas a WordPress desde el frontend Astro.
- **Tailwind CSS**: Para estilos rápidos y responsivos.
- **JavaScript**: Para animaciones y comportamiento dinámico.

---

## 📁 Estructura de Componentes

El sitio se compone de varios componentes:

| Componente              | Descripción |
|------------------------|-------------|
| `HeroComponent.astro`  | Hero section con imagen de fondo y botones de navegación. |
| `VoteComponent.astro`  | Renderiza tarjetas de carros obtenidos desde WordPress con opción de "Votar" y "Ver más". |
| `DiscountComponent.astro` | Sección donde los usuarios pueden acceder a descuentos. |
| `VideoComponent.astro` | Muestra el video destacado extraído desde WordPress por categoría "Video". |
| `FooterComponent.astro` | Footer con logo institucional y textos. |

---

## 🌐 WordPress GraphQL Queries

### Obtener Carros (Categoría: `murga`)
```
query GetPostByCategory {
  posts(where: {categoryName: "murga"}) {
    nodes {
      title
      slug
      date
      excerpt
      featuredImage {
        node {
          sourceUrl
        }
      }
    }
  }
}
```

### Obtener Video Principal (Categoría: Video)
```
query GetVideo {
  posts(where: {categoryName: "Video"}) {
    nodes {
      title
      slug
      excerpt
      date
    }
  }
}
```

### 🖼️ Imágenes y Estilos

Imagen destacada: puq.jpeg utilizada en la sección HeroComponent.
Estilos personalizados: Se cargan desde global.css.

### 🚀 Navegación

El sitio cuenta con navegación interna suave entre secciones utilizando JavaScript:
```
document.querySelectorAll('a[href^="#"]').forEach((anchor) => {
  anchor.addEventListener("click", function (e) {
    e.preventDefault();
    const targetId = this.getAttribute("href").substring(1);
    const targetElement = document.getElementById(targetId);
    if (targetElement) {
      window.scrollTo({
        top: targetElement.offsetTop - 80,
        behavior: "smooth",
      });
    }
  });
});
```

### 🧪 Ejecución local

Instala dependencias:
```
npm install
```
Levanta Astro en modo desarrollo:
```
npm run dev
```
Asegúrate de tener el backend de WordPress activo y accesible en:
```
http://localhost/project-puq/graphql
```

### Datos de la base de datos


// ** Database settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'carnival');

/** Database username */
define('DB_USER', 'user_carnival');

/** Database password */
define('DB_PASSWORD', '20user_carnival25');
