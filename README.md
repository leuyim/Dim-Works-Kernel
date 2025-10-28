# 🚀 Dim Works Kernel Documentation

Dim Works Kernel es una base tecnológica modular, segura y escalable para construir aplicaciones empresariales personalizadas. Este repositorio documenta su arquitectura, instalación, uso y casos de aplicación.

---

## 🧠 ¿Qué es Dim Works Kernel?

Dim Works Kernel es el núcleo de software desarrollado desde 2007 por Dim Works, diseñado para crear soluciones empresariales a medida. A diferencia del software genérico, el Kernel se adapta completamente a las necesidades del negocio.

> “Es como el chasis y motor de un F1: no es un sistema genérico, sino una base lista para construir cualquier solución empresarial.”

### 🔧 Características clave

- Multiusuario en la nube
- Seguridad avanzada (tokens, backups, validación)
- Modularidad total
- Desarrollo rápido (MVP funcional en semanas)
- Iteración continua durante el contrato

---

## 🧩 Aplicaciones construidas con Dim Works Kernel

| 🏭 Sector       | 🧰 Aplicación             | 🔍 Descripción breve |
|----------------|---------------------------|----------------------|
| Agrícola       | PWA Offline               | Evaluación de cultivos sin conexión |
| Logística      | Cadena de Envío           | Gestión de choferes, camiones, kilometraje |
| Manufactura    | Sistema de Calidad 5S     | Evaluación de procesos |
| Finanzas       | Calculadoras de Pronóstico| Estimación de inventario y cotizaciones |
| Retail         | POS y E-commerce          | Ventas, inventario, clientes |
| Corporativo    | ERP y CRM                 | Gestión integral de operaciones |

---

## 📚 Estructura de la Documentación

La documentación se organiza en cinco secciones principales:

### 🧠 (0) Dim Works Kernel

- Introducción al núcleo
- Arquitectura modular
- Seguridad y validación de tokens
- Estructura de archivos y SQLite

### 🛠️ Guía para Desarrolladores

- Desarrollo de módulos
- Integración con APIs externas
- Validación HMAC y autenticación
- Optimización de rendimiento

### 📖 Introducción y Conceptos Clave

- Roles y permisos
- Galerías y estructura de datos
- Lazy loading y eficiencia

### ⚙️ Instalación y Mantenimiento

- Requisitos del sistema
- Instalación paso a paso
- Configuración inicial
- Backup y actualizaciones

### 👥 Manual de Usuario Final

- Subida de archivos e imágenes
- Navegación por galerías
- Gestión de contenido privado y compartido

---

## 💼 Modelo de Negocio

Dim Works ofrece un modelo flexible:

- Inscripción inicial + mensualidades
- MVP funcional desde el mes 1
- Desarrollo iterativo continuo
- Hosting, seguridad y soporte incluidos

### Opciones post-contrato

- 🔄 Continuidad con descuento
- 🛒 Compra total de licencia (buyout)

---

## 📄 Licencia

Este contenido está bajo la **Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License**.

🔗 [Ver términos completos](https://creativecommons.org/licenses/by-nc-nd/4.0/)

---

## 🧑‍💻 Autor y Mantenimiento

Documentación mantenida por [Leuyim](https://github.com/leuyim).  
Dim Works Kernel es un producto privado. Esta documentación es para fines educativos e integrativos.

---

Dim Works Kernel - Documentación Técnica
Tabla de Contenidos
Descripción General

Características Principales

Requisitos del Sistema

Instalación y Configuración

Estructura del Sistema

Uso de Funciones Principales

Gestión de Módulos

Sistema de Seguridad

API y Funcionalidades

Optimización y Rendimiento

Solución de Problemas

Descripción General
Dim Works Kernel es un sistema de gestión de contenido (CMS) y framework PHP de alto rendimiento desarrollado por Dim Works. Proporciona una base sólida para aplicaciones web empresariales con énfasis en seguridad, escalabilidad y mantenibilidad.

Versión Actual: 5.9.999
Última Actualización: 05/09/2025
Desarrollador Principal: Oliver Leuyim Angel

Características Principales
🔒 Seguridad Avanzada (WAF V4)
Firewall de Aplicación Web con detección multi-capa

Rate Limiting inteligente (333 requests/minuto por IP)

Auto-baneo de IPs maliciosas

Protección contra inyecciones SQL y XSS

Geolocalización integrada

Modo aprendizaje para testing

🖼️ Procesamiento de Imágenes
Redimensionamiento automático y optimización

Soporte multi-formato (JPEG, PNG, GIF, WebP, AVIF)

Cache inteligente con expiry de 30 días

Detección automática de capacidades del servidor (Imagick/GD)

📊 Analytics y Logging
Tracking completo de visitas y comportamiento

Métricas de rendimiento en tiempo real

Análisis de dispositivos y navegadores

Sistema de logs estructurado

🗄️ Gestión de Base de Datos
Backup automático con compresión

Sincronización de esquemas

Optimización de índices

Manejo de conexiones eficiente

Requisitos del Sistema
Requisitos Mínimos
bash
PHP >= 8.0.0
MySQL >= 5.7 / MariaDB >= 10.3
Memoria PHP: 128MB mínimo
Extensions: mysqli, gd, json
Requisitos Recomendados
bash
PHP >= 8.1
Memoria PHP: 384MB
Extensions: imagick, curl, gmp, bcmath
Sistema: Linux/Unix
Instalación y Configuración
1. Estructura de Archivos
text
/www/
├── config.php              # Configuración principal
├── securitypars.php        # Parámetros de seguridad
├── incspt/                 # Librerías y dependencias
│   ├── classes/
│   ├── jquery/
│   └── tmp/
├── modulos/                # Módulos de la aplicación
├── bloques/                # Bloques de contenido
├── themes/                 # Temas y plantillas
└── BackUp_DB/              # Respaldos automáticos

Estructura del Sistema
Arquitectura Modular
text
modulos/
├── usuarios/           # Gestión de usuarios
│   ├── config.php
│   ├── Lang/
│   │   ├── es.php
│   │   └── en.php
│   └── notificar.php
├── productos/           # Catálogo de productos
└── blog/                # Sistema de blog
Sistema de Bloques
php
// Posiciones disponibles
bloque2();  // Lateral izquierdo
bloque3();  // Lateral derecho  
bloque4();  // Cabecera
bloque5();  // Pie de página
Gestión de Temas
php
// Configuración de tema

Uso de Funciones Principales
Procesamiento de Imágenes
php
// Uso básico
<img src="?pic=<?= stringDWK_encode('imagen.jpg') ?>&width=800&height=600&compressimg=75">

// Opciones avanzadas
$processor = new ImageProcessor(
    'imagen.jpg',     // URL de imagen
    800,              // Ancho máximo
    600,              // Alto máximo
    75                // Calidad (0-100)
);
$processor->process();
Sistema de Notificaciones
php
// Notificación simple
notificacion(
    "Operación Exitosa",
    "Los cambios se guardaron correctamente",
    "exito",
    "✅",
    5000
);

// Notificación con acciones
notificacion(
    "Confirmación Requerida",
    "¿Está seguro de eliminar este registro?",
    "advertencia",
    "⚠️",
    0,  // Persistente
    [
        [
            'texto' => 'Confirmar',
            'accion' => 'confirmDelete()',
            'clase_css' => 'btn-danger'
        ],
        [
            'texto' => 'Cancelar', 
            'tipo' => 'enlace',
            'url' => '/cancelar'
        ]
    ]
);
Geolocalización
php
// Obtener ubicación
get_location5(true, false);  // defer, required

// En módulos (acceso a variables globales)
global $pais, $ciudad, $codigopostal;
echo "Ubicación: $ciudad, $pais";
Web Push Notifications
php
// Habilitar notificaciones push
JSwebpushSuscript(true, false);  // defer, required

// Enviar campaña push
$campaignId = savePushCampaign(
    "Promoción Especial",
    "¡Oferta por tiempo limitado!",
    "Descuento del 20% en todos los productos",
    "/ofertas",
    "/icon.png",
    'manual',           // Tipo de iniciación
    null,               // Programación (null para inmediato)
    null,               // ID de campaña (null para nueva)
    '{"user_status":"all"}',  // Filtros
    "promo"             // Tag para segmentación
);
Gestión de Módulos
Crear un Nuevo Módulo
1. Estructura del Módulo
text
modulos/mi_modulo/
├── config.php          # Punto de entrada
├── Lang/
│   ├── es.php         # Español
│   └── en.php         # Inglés
├── notificar.php       # Sistema de notificaciones
├── admin/       # administracion
|   ├── nav.php         # menu
│   └── index.php         # panel
└── assets/            # Recursos estáticos
3. Archivo de Configuración Principal
php
<?php
// modulos/mi_modulo/config.php
$titulo_modulo = "Mi Módulo Personalizado";

// Lógica del módulo
if (isset($_GET['ext'])) {
    $extension = $_GET['ext'];
    // Manejar extensiones específicas
    switch($extension) {
        case 'lista':
            include 'lista.php';
            break;
        case 'detalle':
            include 'detalle.php';
            break;
    }
} else {
    // Vista principal del módulo
    echo "<h1>Bienvenido a Mi Módulo</h1>";
    echo "<p>Contenido principal del módulo...</p>";
}
?>
3. Sistema de Traducciones
php
<?php
// modulos/mi_modulo/Lang/es.php
$lang = [
    'welcome' => 'Bienvenido',
    'description' => 'Descripción del módulo',
    'save' => 'Guardar',
    'cancel' => 'Cancelar'
];
?>

<?php
// modulos/mi_modulo/Lang/en.php  
$lang = [
    'welcome' => 'Welcome',
    'description' => 'Module description',
    'save' => 'Save',
    'cancel' => 'Cancel'
];
?>

Solución de Problemas
Errores Comunes y Soluciones
1. Error de Memoria
text
Error: "I_S ML 128M - 64M"
Solución: Aumentar memory_limit en php.ini

ini
memory_limit = 256M
2. Tiempo de Ejecución Excedido
text
Maximum execution time exceeded
Solución: Configurar tiempo máximo

php
ini_set('max_execution_time', 900);
set_time_limit(900);

4. Problemas de Seguridad
Solución: Revisar logs de amenazas

Métricas de Rendimiento


Conclusión
Dim Works Kernel proporciona una base sólida y segura para el desarrollo de aplicaciones web empresariales. Su arquitectura modular, sistema de seguridad avanzado y herramientas de optimización lo hacen adecuado para proyectos de cualquier escala.


Para soporte técnico y actualizaciones, contactar al equipo de desarrollo de Dim Works.

*Documentación técnica para Dim Works Kernel v5.9.999 - Sistema desarrollado por Oliver Leuyim Angel*
