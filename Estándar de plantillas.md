# Dim Works Kernel (DWK)
## Estándar Mínimo Universal de Diseño para Plantillas
**DWK Theme Baseline Standard v1.0**

Este documento define los requisitos mínimos, principios técnicos y criterios de calidad que deben cumplir todas las plantillas compatibles con el ecosistema de Dim Works Kernel (DWK).

El objetivo del estándar es permitir la creación de miles de diseños distintos manteniendo alto rendimiento, compatibilidad multidispositivo, escalabilidad técnica e independencia de frameworks. DWK no estandariza herramientas; estandariza calidad, comportamiento y límites técnicos.

---

## 1. Principios Fundamentales
Toda plantilla DWK debe cumplir de forma estricta con los siguientes principios:

- **Agnosticismo tecnológico:** No depende de una librería, framework o proveedor específico.
- **Performance-first:** Diseñada para alto rendimiento y métricas web modernas medibles.
- **Mobile-first:** Diseño planificado y ejecutado desde resoluciones móviles hacia escritorio.
- **Progressive Enhancement:** Funcionalidad base asegurada sin dependencia crítica de JavaScript.
- **Software libre:** Cero dependencias propietarias o de pago obligatorias.
- **Separación de responsabilidades:** El tema es única y exclusivamente una capa de presentación.

---

## 2. Alcance del Theme (Fronteras de Responsabilidad)

### ✅ El tema PUEDE y DEBE:
- Definir estilos visuales y variables de diseño.
- Estructurar el layout y la retícula.
- Implementar interacciones ligeras de interfaz.
- Adaptarse fluidamente a distintos dispositivos.

### ❌ El tema NO PUEDE bajo ninguna circunstancia:
- Contener lógica de negocio del Kernel.
- Acceder directamente a bases de datos o instanciar conexiones.
- Sobrescribir variables globales del núcleo de DWK.
- Controlar o forzar versiones de dependencias globales del sistema.

---

## 3. Arquitectura Base
La siguiente estructura es recomendada como referencia.
Lo obligatorio es la separación conceptual de activos, no la jerarquía exacta de directorios.

```text
/theme-name/
├── assets/
│   ├── css/
│   │   ├── tokens.css
│   │   ├── base.css
│   │   ├── layout.css
│   │   └── components.css
│   ├── js/
│   │   └── main.js
│   └── img/
├── index.php
├── index_home.html o index_home.php
└── index_sub.html o index_sub.php
```

---

## 4. Estilos y Tokens de Diseño (CSS)

### 4.1 Variables Nativas
Es obligatorio centralizar la identidad visual en la raíz del documento mediante CSS nativo para permitir la manipulación dinámica.
```css
:root {
    /* === 1. DWK Mandatory Baseline Tokens === */
    --dwk-color-bg: #ffffff;
    --dwk-color-text: #1a1a1a;
    --dwk-color-accent: #c5a059;
    --dwk-font-base: 'Montserrat', 'Outfit', system-ui, -apple-system, BlinkMacSystemFont;
    --dwk-radius-base: 12px;

    /* === 2. Paleta de Identidad Emilia Desarrollos === */
    --brand-color: #c5a059;
    --brand-hover: #b38f49;
    --brand-active: #9e7d3a;
    --brand-light: #fcfaf2;
    --brand-gradient: linear-gradient(135deg, #c5a059 0%, #b38f49 100%);
    --brand-shadow: rgba(197, 160, 89, 0.3);

    /* === 3. Fuentes Principales y Secundarias === */
    --font-primary: 'Montserrat', sans-serif;
    --font-secondary: 'Outfit', sans-serif;
    --font-monospace: 'Courier New', Courier, monospace;

    /* === 4. Fuentes y Colores para Encabezados (Titles) === */
    --font-h1: var(--font-primary);
    --font-h1-color: var(--text-primary);
    --font-h1-bg: transparent;
    --font-h1-size: 2.25rem;
    
    --font-h2: var(--font-primary);
    --font-h2-color: var(--text-primary);
    --font-h2-bg: transparent;
    --font-h2-size: 1.75rem;
    
    --font-h3: var(--font-secondary);
    --font-h3-color: var(--brand-color);
    --font-h3-bg: transparent;
    --font-h3-size: 1.5rem;

    --font-h4: var(--font-secondary);
    --font-h4-color: var(--text-secondary);
    --font-h4-bg: transparent;
    --font-h4-size: 1.25rem;

    --font-h5: var(--font-secondary);
    --font-h5-color: var(--text-primary);
    --font-h5-bg: transparent;
    --font-h5-size: 1rem;

    --font-h6: var(--font-secondary);
    --font-h6-color: var(--text-muted);
    --font-h6-bg: transparent;
    --font-h6-size: 0.875rem;

    /* === 5. Layout Base === */
    --bg-primary: #f8fafc;
    --bg-secondary: #ffffff;
    --bg-sidebar: #2d3540;
    --bg-logo: #1e242b;
    --bg-hover: #f1f5f9;
    --bg-active: #e2e8f0;

    /* === 6. Tipografía General y Textos === */
    --text-primary: #1e293b;
    --text-secondary: #475569;
    --text-muted: #64748b;
    --text-inverse: #ffffff;
    --text-accent: #c5a059;
    --text-disabled: #94a3b8;

    /* === 7. Headers & Footers === */
    --header-bg: var(--bg-secondary);
    --header-text: var(--text-primary);
    --header-border: var(--border-color);
    --footer-bg: var(--bg-sidebar);
    --footer-text: var(--text-inverse);
    --footer-border: rgba(255, 255, 255, 0.05);

    /* === 8. Nav Menus & Megamenus === */
    --font-nav: var(--font-primary);
    --nav-bg: transparent;
    --nav-link: rgba(255, 255, 255, 0.75);
    --nav-link-hover: #ffffff;
    --nav-link-active: var(--brand-color);
    --nav-border: rgba(0, 0, 0, 0.15);
    --megamenu-bg: var(--bg-secondary);
    --megamenu-item-hover: var(--bg-hover);
    --megamenu-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
    --megamenu-border: var(--border-color);

    /* === 9. Sidebars === */
    --font-sidebar: var(--font-secondary);
    --sidebar-bg: #2d3540;
    --sidebar-text: rgba(255, 255, 255, 0.75);
    --sidebar-link: rgba(255, 255, 255, 0.75);
    --sidebar-link-hover: #ffffff;
    --sidebar-link-active: var(--brand-color);
    --sidebar-border: rgba(0, 0, 0, 0.2);

    /* === 10. Modals === */
    --font-modal: var(--font-primary);
    --modal-bg: var(--bg-secondary);
    --modal-backdrop: rgba(0, 0, 0, 0.5);
    --modal-border: var(--border-color);
    --modal-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
    --modal-header-bg: var(--bg-primary);
    --modal-footer-bg: var(--bg-primary);
    --modal-text: var(--text-primary);

    /* === 11. Copyright === */
    --copyright-bg: transparent;
    --copyright-text: rgba(255, 255, 255, 0.55);
    --copyright-border: rgba(0, 0, 0, 0.2);

    /* === 12. Notifications & Alerts === */
    --font-alert: var(--font-secondary);
    --notif-bg: var(--bg-secondary);
    --notif-text: var(--text-primary);
    --notif-border: var(--border-color);
    --alert-success-bg: #ecfdf5;
    --alert-success-text: #047857;
    --alert-success-border: #a7f3d0;
    --alert-danger-bg: #fef2f2;
    --alert-danger-text: #b91c1c;
    --alert-danger-border: #fecaca;
    --alert-warning-bg: #fffbeb;
    --alert-warning-text: #b45309;
    --alert-warning-border: #fde68a;
    --alert-info-bg: #eff6ff;
    --alert-info-text: #1d4ed8;
    --alert-info-border: #bfdbfe;

    /* === 13. Tables === */
    --font-table: var(--font-secondary);
    --table-bg: var(--bg-secondary);
    --table-header-bg: var(--bg-primary);
    --table-header-text: var(--text-muted);
    --table-row-even: var(--bg-primary);
    --table-row-odd: var(--bg-secondary);
    --table-row-hover: var(--bg-hover);
    --table-border: var(--border-color);

    /* === 14. Forms & Inputs (Text, Select, Date, Mail, Number) === */
    --font-form: var(--font-secondary);
    --input-bg: #ffffff;
    --input-text: var(--text-primary);
    --input-border: var(--border-color);
    --input-focus-border: var(--brand-color);
    --input-focus-shadow: 0 0 0 4px rgba(197, 160, 89, 0.15);
    --input-placeholder: var(--text-muted);
    --input-disabled-bg: var(--bg-active);
    --input-disabled-text: var(--text-disabled);
    --input-select-bg: #ffffff;
    --input-date-bg: #ffffff;
    --input-mail-bg: #ffffff;
    --input-number-bg: #ffffff;

    /* === 15. Paginación === */
    --font-pagination: var(--font-primary);
    --pagination-bg: var(--bg-primary);
    --pagination-text: var(--text-secondary);
    --pagination-hover-bg: var(--bg-hover);
    --pagination-hover-text: var(--brand-color);
    --pagination-active-bg: var(--brand-color);
    --pagination-active-text: var(--text-inverse);
    --pagination-border: var(--border-color);

    /* === 16. Logos e Imagotipos === */
    --logo-width: 100%;
    --logo-filter: none;
    --imagotipo-color: var(--brand-color);
    --logo-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);

    /* === 17. Bloques, Galerías y Carouseles === */
    --block-bg: var(--bg-secondary);
    --block-padding: 2rem;
    --block-border: var(--border-color);
    --block-radius: var(--radius-card);
    --block-shadow: var(--s-card);
    
    --gallery-grid-gap: 1.5rem;
    --gallery-item-radius: var(--radius-card);
    --gallery-item-hover-scale: 1.05;
    --gallery-caption-bg: rgba(0, 0, 0, 0.7);
    --gallery-caption-text: #ffffff;
    
    --carousel-nav-bg: rgba(255, 255, 255, 0.8);
    --carousel-nav-hover-bg: #ffffff;
    --carousel-indicator-bg: rgba(255, 255, 255, 0.4);
    --carousel-indicator-active-bg: var(--brand-color);

    /* === 18. HR (Horizontal Rule) === */
    --hr-border: var(--border-color);
    --hr-margin: 1.75rem 0;

    /* === 19. LI (Lists) === */
    --li-bullet-color: var(--brand-color);
    --li-hover-bg: var(--bg-hover);
    --li-spacing: 0.5em;

    /* === 20. Buttons === */
    --font-btn: var(--font-primary);
    --btn-bg: var(--brand-color);
    --btn-text: var(--text-inverse);
    --btn-hover-bg: var(--brand-hover);
    --btn-active-bg: var(--brand-active);
    --btn-disabled-bg: var(--text-disabled);
    --btn-alt-bg: #475569;
    --btn-alt-text: var(--text-inverse);
    --btn-alt-hover: #334155;

    /* === 21. Links & Hovers === */
    --link-color: var(--brand-color);
    --link-hover-color: var(--brand-hover);
    --link-active-color: var(--brand-active);

    /* === 22. Icons & Emojis === */
    --icon-color: var(--brand-color);
    --icon-hover-color: var(--brand-hover);
    --emoji-size: 1.2rem;
    --emoji-opacity: 0.9;

    /* === 23. Shadows, Borders & Radius === */
    --border-color: #e2e8f0;
    --border-light: #f1f5f9;
    --border-dark: #cbd5e1;
    --border-focus: var(--brand-color);
    --outline-color: rgba(197, 160, 89, 0.2);
    
    --radius-card: 12px;
    --radius-btn: 50px;
    --radius-input: 8px;
    --radius-small: 4px;
    
    --s-premium: 0 10px 25px rgba(0, 0, 0, 0.03);
    --s-card: 0 4px 6px rgba(0, 0, 0, 0.05);
    --s-dropdown: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
    --s-inner: inset 0 2px 4px 0 rgba(0, 0, 0, 0.06);

    /* === 24. Navigation & Sidebar specific === */
    --nav-item-bg-hover: rgba(255, 255, 255, 0.05);
    --nav-item-bg-active: rgba(197, 160, 89, 0.15);
    --nav-item-text: rgba(255, 255, 255, 0.75);
    --nav-item-active-text: #ffffff;
}
```
En caso de requerir la carga de librerías de terceros (Bootstrap, Tailwind, etc.), estas deben ser referenciadas mediante etiquetas `<script>` o `<link>` en las secciones correspondientes de la plantilla, sin alterar el DOM o el flujo de control del Kernel.

Los tokens deben permitir la extensión futura a esquemas como dark mode o high‑contrast.

Para el uso de **jQuery** y **jQueryUI** se deben utilizar las funciones nativas del Kernel.  
Para integraciones de geolocalización y notificaciones web push también deben usarse las funciones nativas del Kernel, así como las variables globales como `$page_url`, `$base_url`, `$theme_path`, etc.

### 4.2 Responsividad
- Enfoque exclusivo Mobile-first.
- Uso de Media Queries estándar (`@media (min-width: ...)`).
- Prohibido el uso de JavaScript para manipular o recalcular el layout base.

---

## 5. Frameworks CSS y Librerías
DWK no posee ni impone un framework oficial.

- **Nivel 1 (Ideal):** CSS puro, Vanilla Grid, Flexbox nativo.
- **Nivel 2 (Aceptado):** Frameworks ligeros sin dependencias (Pico.css, Chota).
- **Nivel 3 (Condicionado):** Tailwind CSS o Bootstrap. Solo se aceptan si se entregan los archivos CSS finales completamente purgados (sin clases no utilizadas) y minificados. Cero dependencias de su respectivo JS para la estructura.

DWK no asume ni requiere el uso de herramientas de build (Node.js, npm, bundlers). Su uso queda a criterio del autor del tema.

---

## 6. Recursos Multimedia y Fuentes

### 6.1 Tipografía
- Prioridad a fuentes del sistema (`system-ui`).
- Toda fuente externa debe ser libre y utilizar obligatoriamente la regla `font-display: swap;`.
- Prohibidas las fuentes bloqueantes que generen FOUT prolongados.

### 6.2 Iconografía
- Estándar obligatorio: Iconos **SVG en línea**.
- Librerías sugeridas: Tabler Icons, Lucide Icons, Remix Icon.
- Si un icono puede implementarse directamente en el DOM como SVG, no debe llamarse mediante una petición a una fuente completa (Webfont).

---

## 7. JavaScript e Interactividad
- Prioridad a Vanilla JS.
- Todo script propio debe cargarse con los atributos `defer` o `async`.
- Estrictamente prohibido el uso de JavaScript crítico para habilitar la navegación básica del sitio.

---

## 8. Métricas de Rendimiento (Estándar de Certificación)
Para que un tema sea considerado "DWK Compatible", debe someterse a auditoría y no exceder los siguientes límites en producción.  
Las métricas siguientes representan los objetivos de calidad que un theme DWK debe estar diseñado para alcanzar, sin introducir prácticas que degraden el rendimiento.

| Métrica de Evaluación | Límite / Objetivo Obligatorio |
| :--- | :--- |
| **Lighthouse: Performance** | ≥ 95 |
| **Lighthouse: Accessibility** | ≥ 95 |
| **Peso Total de CSS** | ≤ 150 KB |
| **Peso Total de JS propio** | ≤ 100 KB |
| **Formatos de Imagen** | WebP o SVG nativo |

---

## 9. PWA y Accesibilidad
- **PWA-Ready:** Soporte nativo para lectura de `manifest.json` y metadatos `theme-color`. El tema no debe romperse si el Service Worker no está disponible.
- **Accesibilidad (WCAG AA):** Uso estricto de HTML semántico, navegación habilitada por teclado en menús principales y contraste de color que apruebe validaciones automatizadas.

---

## 10. Integración con el Kernel
- La carga de librerías comunes de administración será inyectada dinámicamente por las rutinas del `index.php` del núcleo, no forzadas por el tema.

---

## X. Reglas Obligatorias de Renderizado (HEAD y BODY)

Dim Works Kernel define un conjunto de funciones **obligatorias** que forman parte del contrato entre el Kernel y cualquier theme compatible.  
El tema no debe alterar ni redefinir estas funciones, únicamente invocarlas en los puntos correctos del documento.

---

### X.1 Estructura Obligatoria del `<head>`

Todo theme DWK **debe renderizar y permitir** la siguiente estructura mínima en el `<head>` del documento:

- Título dinámico gestionado por el Kernel  
- Base URL del theme  
- Metadatos SEO fundamentales  
- Inyección de librerías, APIs y configuraciones globales  

Implementación obligatoria:

```php
<title><?php
    if (empty($mod_name)) {
        echo $page_name;
    } else {
        print $page_name . " - " . $mod_name;
    }
?></title>

<base href="<?php print $page_url; ?>themes/<?php print $patheme; ?>/" />
<meta name="description" content="<?php print $descript; ?>" />
<meta name="keywords" content="<?php print $gkeyword; ?>" />

<?php jquery(); ?>
<?php get_location5(); ?>
<?php googleapi(); ?>
<?php print $verify; ?>
<?php setfeeds(); ?>
<?php multilng(); ?>
<?php facebookconnect(); ?>
```
Estas funciones:
- Son controladas exclusivamente por el Kernel  
- No deben ser reemplazadas, eliminadas o redefinidas por el theme  

---

### X.2 Renderizado Obligatorio del Contenido Principal

Todo theme DWK debe incluir obligatoriamente la función:
```php
<?php bodymodule(); ?>
```
Esta función es responsable de renderizar la totalidad del contenido dinámico generado por los módulos del sistema.  
Un theme que no incluya `bodymodule()` no es considerado compatible con DWK.

---

### X.3 Bloques Genéricos (Opcionales)

DWK permite el uso de bloques genéricos para composición de layout, por ejemplo:
```php
<?php 
bloque2();
bloque3();
bloque4(); 
bloque5();
?>
```
Reglas:
- Los bloques son opcionales  
- El theme puede incluirlos o no  
- El Kernel no depende de su existencia  
- No deben ser obligatorios para el funcionamiento del sitio

## XI. Reglas de Estilización de Elementos HTML/HTML5

Todo template DWK debe generar y aplicar CSS para **todos los elementos estándar de HTML y HTML5**, incluyendo encabezados (`h1`, `h2`, ...), párrafos (`p`), listas (`ul`, `ol`, `li`), formularios (`form`), campos (`input`, `textarea`, `select`, `button`), tablas (`table`, `thead`, `tbody`, `tr`, `td`, `th`), contenedores (`div`, `span`), y demás etiquetas semánticas.

Los estilos deben aplicarse de forma directa a los selectores de elementos o, en su caso, dentro de un contenedor definido por el tema. Ejemplo:
```php
<div class="wrapper">
  <?php bodymodule(); ?>
</div>
```
El CSS puede implementarse como:
```css
.wrapper h1 { /* estilos para h1 dentro del contenedor */ }
```
o bien de manera tajante:
```css
h1 { /* estilos globales para h1 */ }
```
Reglas:
- El theme debe cubrir todos los elementos básicos para que los módulos del Kernel puedan heredar estilos consistentes.
- No se permite depender exclusivamente de clases externas; los estilos deben estar definidos para los elementos nativos.
- La ausencia de esta guía mínima invalida la certificación DWK del theme.

### XI.1 Archivo de Guía Obligatorio

Cada theme DWK debe incluir un archivo llamado `codes.php` o `codes.html` en el cual se documente y muestre:

- La guía completa de todos los elementos estilizados (divs, spans, títulos, listas, formularios, inputs, tablas, etc.).
- Ejemplos de uso de librerías permitidas y su integración correcta.
- Comportamientos y menucidades del template (hover, focus, active, disabled, etc.).
- Detalles de implementación para **desktop y mobile**, asegurando consistencia en ambos entornos.
- Instrucciones claras para que cualquier desarrollador pueda usar e implementar el tema sin ambigüedades.

Reglas:
- El archivo debe ser autoexplicativo y contener ejemplos prácticos.
- No debe incluir lógica de negocio ni dependencias externas.
- La ausencia de este archivo invalida la certificación DWK del theme.
