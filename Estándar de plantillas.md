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
├── manifest.json
├── sw.js
└── theme.info.php
```

---

## 4. Estilos y Tokens de Diseño (CSS)

### 4.1 Variables Nativas
Es obligatorio centralizar la identidad visual en la raíz del documento mediante CSS nativo para permitir la manipulación dinámica.
```css
:root {
  --dwk-color-bg: #ffffff;
  --dwk-color-text: #1a1a1a;
  --dwk-color-accent: #0d6efd;
  --dwk-font-base: system-ui, -apple-system, BlinkMacSystemFont;
  --dwk-radius-base: 8px;
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
