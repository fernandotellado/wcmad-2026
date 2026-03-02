# SEO y GEO en WordPress sin plugins de SEO

**Taller impartido en WordCamp Madrid 2026 por Fernando Tellado**
[AyudaWP.com](https://ayudawp.com) · [@fernandot](https://x.com/fernandot)

> ¿Yoast, Rank Math, All in One SEO, SEOPress… o la nada?
> Resulta que hay un mundo de posibilidades para posicionar en Google y en la IA generativa sin plugins de SEO, y mucho menos pagar por ello.

---

## 1. WordPress ya hace SEO por ti

La mayoría de funciones que ofrecen los plugins de SEO ya las tienes en WordPress de serie. Solo hay que saber dónde están.

### Ajustes de lectura — Visibilidad en buscadores

En **Ajustes → Lectura** existe el checkbox *"Disuade a los motores de búsqueda de indexar este sitio"*. Al activarlo, WordPress añade un `noindex` a **todo** el sitio. Es habitual dejarlo marcado por error, sobre todo en migraciones de staging a producción. Compruébalo siempre.

### Títulos y slugs

WordPress genera automáticamente los títulos `<title>` y los permalinks. No necesitas un plugin para eso. Lo que sí debes hacer:

- Editar el slug para que sea corto, descriptivo y con la palabra clave
- Usar la estructura de permalinks `/%postname%/` (Ajustes → Enlaces permanentes)
- No dejar que WordPress genere slugs con números o textos sin sentido

### Sitemap nativo

Desde WordPress 5.5, tu sitio ya tiene un mapa del sitio en `/wp-sitemap.xml`. Incluye entradas, páginas, categorías, etiquetas y tipos de contenido personalizados.

**¿Qué le falta?** Control sobre qué se incluye y qué no. Para eso puedes usar [Native Sitemap Customizer](https://wordpress.org/plugins/native-sitemap-customizer/), que te permite excluir tipos de contenido, taxonomías o entradas concretas.

Más info: [Personalizar el sitemap nativo de WordPress](https://ayudawp.com/plugin-personalizar-sitemap-nativo-wordpress/)

### Robots.txt virtual

WordPress genera un `robots.txt` virtual accesible añadiendo `?robots=1` a la URL de tu sitio (por ejemplo `tusitio.com/?robots=1`). Casi nadie sabe que existe. Contiene las reglas básicas y enlaza el sitemap.

Si necesitas más control (bloquear rastreadores de IA, añadir reglas específicas), [AI Content Signals](https://wordpress.org/plugins/ai-content-signals/) lo detecta y te permite crear un robots.txt físico personalizado.

**Herramienta de ayuda:** [Checker y generador de robots.txt](https://herramientas.ayudawp.com/#robots-txt)

### Ajustes de comentarios

Los comentarios son contenido fresco y señal de engagement, pero si no los controlas te llenan de enlaces basura. En **Ajustes → Comentarios** revisa:

- Moderación de comentarios con enlaces (puedes limitar cuántos enlaces se permiten antes de ir a moderación)
- Lista negra de palabras y URLs
- Aprobación manual del primer comentario de cada usuario

### wp-config.php

Unas líneas en `wp-config.php` pueden ayudar al rendimiento y, por tanto, al SEO:

- `define('WP_POST_REVISIONS', 5);` — Limitar revisiones de entradas
- `define('AUTOSAVE_INTERVAL', 120);` — Reducir la frecuencia de autoguardado (en segundos)
- `define('EMPTY_TRASH_DAYS', 15);` — Vaciar papelera más a menudo

**Herramienta de ayuda:** [Generador de wp-config.php](https://herramientas.ayudawp.com/#wp-config)

---

## 2. Performance: lo que rompe tu SEO sin que lo sepas

Antes de preocuparte por lo que escribes, asegúrate de que tu sitio carga bien. Google lo mide y las IAs también.

### TTFB (Time to First Byte)

Es el tiempo que tarda tu servidor en responder con el primer byte. Es la métrica más ignorada y una de las más importantes. Si tu TTFB es alto, da igual lo bien que optimices el frontend.

Cómo comprobarlo:

- DevTools del navegador → pestaña Network → primer request → columna "Waiting (TTFB)"
- PageSpeed Insights lo reporta en las métricas del servidor

Un buen TTFB debería estar por debajo de 200 ms. Si supera los 600 ms, tienes un problema de servidor o de código.

Más info: [Todo sobre el TTFB](https://ayudawp.com/ttfb/)

### Límite de rastreo (Crawl Budget)

Google tiene un límite de cuántas páginas rastreará de tu sitio. Si tienes muchas URLs innecesarias (archivos de autor, archivos de fecha, páginas de adjuntos, paginaciones infinitas…), estás desperdiciando ese presupuesto de rastreo en páginas que no aportan nada.

El sitemap de WordPress no puede superar los **2 MB** ni las **50.000 URLs**. Si te acercas a esos límites, tienes que limpiar.

**Herramienta de ayuda:** [Analizador de límite de rastreo](https://herramientas.ayudawp.com/#crawl-limit)

### Cachés: las 3 capas que debes conocer

- **Caché de página:** almacena el HTML generado para no ejecutar PHP+MySQL en cada visita. Plugins como WP Super Cache, Cache Enabler o el Speed Optimizer de SiteGround
- **Caché de objetos:** almacena resultados de consultas a base de datos. Memcached o Redis (muchos hostings ya lo ofrecen, solo hay que activarlo)
- **Caché de navegador:** le dice al navegador del visitante que guarde archivos estáticos. Se configura desde el servidor o `.htaccess`

### Limpieza con WPO Tweaks

[Zero Config Performance Optimization](https://wordpress.org/plugins/wpo-tweaks/) desactiva funciones de WordPress que no necesitas y que ralentizan tu sitio:

- Emojis inline (sí, WordPress carga un script para emojis)
- oEmbed/Embeds innecesarios
- Query strings en archivos estáticos
- API REST para usuarios no autenticados
- Y montones más

### Cron limpio

WordPress tiene un sistema de tareas programadas (WP-Cron) que acumula basura con el tiempo. Plugins desinstalados que dejan tareas huérfanas, ejecuciones duplicadas…

[Easy Actions Scheduler Cleaner](https://wordpress.org/plugins/easy-actions-scheduler-cleaner-ayudawp/) te muestra qué hay programado y te deja limpiarlo.

---

## 3. Tu contenido es tu SEO/GEO: el editor como herramienta

### Visualizador de estructura

El editor de bloques tiene un panel de estructura (icono de "i" o el outline en la barra superior) que te muestra:

- Conteo de palabras, caracteres, bloques y encabezados
- Esquema jerárquico de encabezados (H2, H3, H4…)
- Saltos de jerarquía (si pasas de H2 a H4 sin H3)

Úsalo antes de publicar como checklist rápido.

### Encabezados con jerarquía

- H1: solo el título de la entrada (WordPress ya lo pone)
- H2: secciones principales
- H3: subsecciones dentro de un H2
- No saltar niveles (de H2 a H4 directamente)
- Incluir palabras clave de forma natural, no forzada

### Texto alternativo en imágenes

El campo "Texto alternativo" en las imágenes es uno de los factores SEO más ignorados. Describe lo que se ve en la imagen de forma concisa. No lo dejes vacío, no metas palabras clave a saco, describe la imagen.

### Extracto manual

Si no rellenas el extracto manualmente, WordPress genera uno automático recortando el contenido. Ese extracto muchas veces acaba como meta description en los resultados de búsqueda. Mejor controlarlo tú.

### Relaciones de enlace

Al insertar un enlace en el editor de bloques, puedes añadir atributos `rel`:

- `nofollow`: para enlaces que no quieres que transfieran autoridad
- `sponsored`: para enlaces patrocinados o de afiliación
- `ugc`: para contenido generado por usuarios

WordPress ya te deja hacer esto sin plugin. Úsalo.

### El bloque "Leer más"

El bloque "Más" (More) controla dónde se corta la vista previa de tu entrada en archivos y portada. Un buen corte mejora el CTR porque invita a hacer clic.

[SEO Read More Buttons](https://wordpress.org/plugins/seo-read-more-buttons-ayudawp/) te da más control sobre el texto y estilo de estos botones.

Más info: [SEO Read More Buttons](https://ayudawp.com/seo-read-more-buttons/)

### Cómo escribir para que las IAs te citen

Las IAs no leen como un humano que escanea la página buscando lo que le interesa. Procesan 
el texto de forma secuencial, de principio a fin, y priorizan lo que encuentran primero. 
Esto cambia completamente cómo deberías estructurar tus contenidos.

**La cápsula de respuesta: tus primeras 50-70 palabras**

Es el concepto más importante. Cada artículo o página debería responder la pregunta 
principal en las primeras 50 a 70 palabras, antes de desarrollar nada más. Las IAs 
extraen principalmente de ese primer fragmento.

Estructura ideal: encabezado con la pregunta → respuesta directa en 1-2 frases → dato 
de apoyo → y ya después todo el desarrollo que quieras.

**Malo:** "Hoy en día tener una tienda online es fundamental para cualquier negocio. 
En este artículo vamos a ver cómo..." (relleno antes de responder).

**Bueno:** "Crear una tienda online con WooCommerce cuesta entre 0 € y 5.000 €, 
dependiendo de si la haces tú o contratas a un profesional. El coste mínimo real 
ronda los 100 €/año." (respuesta directa con dato concreto).

**Datos concretos, no generalidades**

Las IAs priorizan contenido con datos verificables y específicos. Si incluyes cifras, 
porcentajes, fechas y fuentes, tienes más probabilidad de ser citado que con 
afirmaciones vagas.

"Las AI Overviews están aumentando mucho" → no te van a citar.
"Las AI Overviews aparecen en el 30% de las búsquedas según SE Ranking (2025)" → 
esto sí es citable.

**Las consultas largas son tu mejor oportunidad**

Las búsquedas de 8 o más palabras tienen hasta 7 veces más probabilidad de activar 
respuestas de IA que las de 1-2 palabras. "hosting WordPress" es muy difícil, pero 
"mejor hosting para WordPress con mucho tráfico en España" es una oportunidad real.

**Contenido multimodal: texto + imágenes + vídeo**

Las páginas que combinan texto, imágenes propias y vídeo tienen un 156% más de 
probabilidad de ser mencionadas por las IAs. Nada de fotos decorativas de stock: 
capturas de pantalla propias, diagramas que expliquen algo, vídeos de demostración.

**Usa preguntas como encabezados**

Usa preguntas frecuentes como H2 o H3 siempre que sea natural. Coincide directamente 
con cómo buscan los usuarios y facilita que las IAs extraigan la respuesta.

**Pilas temáticas: no publiques artículos sueltos**

Las IAs favorecen sitios que demuestran cobertura completa de un tema. Una página 
principal exhaustiva + artículos satélite específicos + enlazado interno entre todos 
ellos señala autoridad temática. No eres alguien que escribió un artículo, eres 
alguien que domina el tema.

---

## 4. GEO: preparar tu WordPress para la IA generativa

El SEO clásico optimiza para buscadores. El GEO (Generative Engine Optimization) optimiza para que las IAs entiendan, citen y recomienden tu contenido.

### El contexto: qué está pasando

Google ya muestra AI Overviews (resúmenes generados por IA) en los resultados de búsqueda. ChatGPT, Perplexity, Claude y otros asistentes rastrean la web para generar respuestas. Tu contenido ya está siendo consumido por IAs, la cuestión es si les estás facilitando el trabajo o no.

Más info:
- [SEO e IA: todo lo que necesitas saber](https://ayudawp.com/seo-ia/)
- [El gran desacoplamiento de Google](https://ayudawp.com/gran-desacoplamiento-google/)
- [AI Overviews de Google](https://ayudawp.com/ai-overviews-google/)

### JSON-LD / Datos estructurados

Los datos estructurados en formato JSON-LD son el idioma que entienden tanto Google como las IAs. Le dicen a las máquinas qué tipo de contenido es tu página (artículo, producto, receta, FAQ…), quién lo ha escrito, cuándo, etc.

[VigIA](https://wordpress.org/plugins/vigia/) genera automáticamente el JSON-LD para tu contenido WordPress.

Más info: [JSON-LD en WordPress](https://ayudawp.com/json-ld/)

### llms.txt y llms-full.txt

Es un estándar emergente que permite a las IAs entender la estructura completa de tu sitio de un vistazo. Similar al `robots.txt` pero pensado para modelos de lenguaje.

- `llms.txt`: resumen de la estructura del sitio
- `llms-full.txt`: versión completa con todo el contenido

[VigIA](https://wordpress.org/plugins/vigia/) los genera automáticamente para tu WordPress.

Más info: [Todo sobre llms.txt y llms-full.txt](https://ayudawp.com/llms-txt-llms-full-txt/)

### Markdown para agentes IA

Las IAs procesan el contenido en formato Markdown mucho mejor que el HTML. Si ofreces una versión Markdown de tus contenidos, les facilitas el trabajo y aumentas las probabilidades de que te citen correctamente.

[VigIA](https://wordpress.org/plugins/vigia/) también genera versiones Markdown de tus contenidos accesibles para agentes de IA.

Más info: [Markdown para agentes IA](https://ayudawp.com/markdown-agentes-ia/)

### AI Content Signals

La iniciativa de Cloudflare para estandarizar cómo los sitios web comunican sus preferencias a los rastreadores de IA. Tu sitio puede indicar si permite o no el rastreo por IA, bajo qué condiciones, y con qué propósito.

[AI Content Signals](https://wordpress.org/plugins/ai-content-signals/) implementa esto en WordPress, además de ayudarte a crear un `robots.txt` físico personalizado.

Más info: [AI Content Signals](https://ayudawp.com/ai-content-signals-el-plugin-wordpress-gratuito-que-facilita-la-adopcion-de-la-iniciativa-de-cloudflare/)

### AI Share & Summarize

Facilita que las IAs puedan compartir y resumir tu contenido de forma correcta, con la atribución adecuada.

[AI Share & Summarize](https://wordpress.org/plugins/ai-share-summarize/)

Más info: [AI Share & Summarize](https://ayudawp.com/ai-share-summarize/)

### Analítica de bots IA

¿Sabes qué bots de IA están rastreando tu sitio? Probablemente no. [VigIA](https://wordpress.org/plugins/vigia/) registra las visitas de bots de IA (GPTBot, ClaudeBot, PerplexityBot…) para que sepas quién consume tu contenido.

Si no sabes quién te visita, no puedes optimizar para ellos.

Más info: [VigIA - analítica y herramientas GEO](https://ayudawp.com/vigia/)

---

## Bonus: lo que no dio tiempo en el taller

### Seguridad premium pero gratis: Vigilante

La seguridad afecta indirectamente al SEO. Un sitio hackeado acaba en la lista negra de Google. [Vigilante](https://wordpress.org/plugins/vigilante/) añade capas de protección completas sin complicaciones.

### Control de visibilidad de contenidos

A veces necesitas controlar qué contenido se muestra y cuándo, sin que los buscadores indexen cosas que no deberían:

- [Scheduled Posts Showcase](https://wordpress.org/plugins/scheduled-posts-showcase/) — Muestra entradas programadas de forma controlada
- [Widget Visibility Control](https://wordpress.org/plugins/widget-visibility-control/) — Controla dónde se muestran los widgets
- [Post Visibility Control](https://wordpress.org/plugins/post-visibility-control/) — Controla la visibilidad de entradas por rol, fecha, etc.

### Tips de htaccess para SEO

El archivo `.htaccess` permite configuraciones avanzadas de redirecciones, cabeceras de caché y seguridad a nivel de servidor.

**Herramienta de ayuda:** [Generador de .htaccess](https://herramientas.ayudawp.com/#htaccess)

### Optimización de imágenes antes de subir

Las imágenes sin optimizar son una de las principales causas de sitios lentos. Optimízalas antes de subirlas a WordPress, no después con plugins que consumen recursos del servidor.

**Herramienta de ayuda:** [Optimizador de imágenes](https://herramientas.ayudawp.com/#imagenes)

### SEO específico para WooCommerce

Si tienes una tienda online, hay optimizaciones adicionales:

- [Descripciones de productos con IA](https://ayudawp.com/descripciones-woocommerce-ia/)
- [Tus productos en ChatGPT](https://ayudawp.com/productos-woocommerce-chatgpt/)
- [Recomendaciones de IA para tu tienda](https://ayudawp.com/recomendaciones-ia/)

---

## Herramientas mencionadas

### Herramientas online gratuitas (AyudaWP)

| Herramienta | Enlace |
|---|---|
| Checker y generador de robots.txt | [herramientas.ayudawp.com/#robots-txt](https://herramientas.ayudawp.com/#robots-txt) |
| Analizador de límite de rastreo | [herramientas.ayudawp.com/#crawl-limit](https://herramientas.ayudawp.com/#crawl-limit) |
| Optimizador de imágenes | [herramientas.ayudawp.com/#imagenes](https://herramientas.ayudawp.com/#imagenes) |
| Generador de wp-config.php | [herramientas.ayudawp.com/#wp-config](https://herramientas.ayudawp.com/#wp-config) |
| Generador de .htaccess | [herramientas.ayudawp.com/#htaccess](https://herramientas.ayudawp.com/#htaccess) |
| Optimizador de prompts para IA | [herramientas.ayudawp.com/#prompt-optimizer](https://herramientas.ayudawp.com/#prompt-optimizer) |

### Plugins WordPress gratuitos

| Plugin | Para qué sirve |
|---|---|
| [VigIA](https://wordpress.org/plugins/vigia/) | JSON-LD, llms.txt, Markdown para IAs, analítica de bots IA |
| [AI Content Signals](https://wordpress.org/plugins/ai-content-signals/) | Señales para rastreadores IA, robots.txt físico |
| [AI Share & Summarize](https://wordpress.org/plugins/ai-share-summarize/) | Compartir y resumir contenido para IAs |
| [Native Sitemap Customizer](https://wordpress.org/plugins/native-sitemap-customizer/) | Personalizar el sitemap nativo de WordPress |
| [SEO Read More Buttons](https://wordpress.org/plugins/seo-read-more-buttons-ayudawp/) | Control de botones "Leer más" |
| [WPO Tweaks](https://wordpress.org/plugins/wpo-tweaks/) | Optimización de rendimiento |
| [Easy Actions Scheduler Cleaner](https://wordpress.org/plugins/easy-actions-scheduler-cleaner-ayudawp/) | Limpieza del cron de WordPress |
| [Vigilante](https://wordpress.org/plugins/vigilante/) | Seguridad básica |
| [Scheduled Posts Showcase](https://wordpress.org/plugins/scheduled-posts-showcase/) | Mostrar entradas programadas |
| [Widget Visibility Control](https://wordpress.org/plugins/widget-visibility-control/) | Control de visibilidad de widgets |
| [Post Visibility Control](https://wordpress.org/plugins/post-visibility-control/) | Control de visibilidad de entradas |

---

## Snippets para wp-config.php

Copia y pega estos fragmentos en tu archivo `wp-config.php`, justo **antes** de la línea `/* That's all, stop editing! */`. Adapta los valores a tu caso.

**Herramienta de ayuda:** [Generador de wp-config.php de AyudaWP](https://herramientas.ayudawp.com/#wp-config)

### Limitar revisiones de entradas

Por defecto WordPress guarda todas las revisiones de cada entrada, lo que infla la base de datos. Limítalo a un número razonable.

```php
// Guardar solo las últimas 5 revisiones por entrada
define( 'WP_POST_REVISIONS', 5 );
```

### Reducir la frecuencia de autoguardado

WordPress autoguarda cada 60 segundos. Si tienes muchos editores simultáneos o un hosting modesto, reduce la carga.

```php
// Autoguardado cada 120 segundos (por defecto 60)
define( 'AUTOSAVE_INTERVAL', 120 );
```

### Vaciar la papelera antes

La papelera acumula contenido durante 30 días por defecto. Reducirlo libera espacio en base de datos.

```php
// Vaciar papelera cada 15 días (por defecto 30)
define( 'EMPTY_TRASH_DAYS', 15 );
```

### Desactivar el editor de archivos del admin

Evita que cualquier usuario con acceso al admin pueda editar archivos PHP de plugins y temas directamente. Es una medida de seguridad básica.

```php
// Desactivar editor de archivos en el panel de administración
define( 'DISALLOW_FILE_EDIT', true );
```

### Forzar SSL en el área de administración

Si ya tienes certificado SSL (y deberías), fuerza que el admin siempre use HTTPS.

```php
// Forzar HTTPS en wp-admin y wp-login.php
define( 'FORCE_SSL_ADMIN', true );
```

### Desactivar el cron nativo de WordPress

El cron de WordPress se ejecuta en cada visita, lo que puede ralentizar la carga. La alternativa es configurar un cron real en tu servidor (cPanel, Plesk o similar) apuntando a `wp-cron.php`.

```php
// Desactivar WP-Cron (configurar cron real en el servidor)
define( 'DISABLE_WP_CRON', true );
```

### Aumentar el límite de memoria PHP

Si tu sitio se queda sin memoria en operaciones pesadas (importaciones, WooCommerce con muchos productos), auméntalo.

```php
// Memoria para el frontend
define( 'WP_MEMORY_LIMIT', '256M' );
// Memoria para el área de administración
define( 'WP_MAX_MEMORY_LIMIT', '512M' );
```

### Activar la concatenación y compresión de scripts

Reduce el número de peticiones HTTP en el panel de administración concatenando y comprimiendo los archivos JS y CSS.

```php
// Concatenar y comprimir scripts y estilos en el admin
define( 'CONCATENATE_SCRIPTS', true );
define( 'COMPRESS_SCRIPTS', true );
define( 'COMPRESS_CSS', true );
```

---

## Snippets para .htaccess

Estos fragmentos van en el archivo `.htaccess` de la raíz de tu WordPress. Añádelos **después** de las reglas de WordPress (el bloque `# BEGIN WordPress` / `# END WordPress`), nunca dentro de ese bloque porque WordPress lo puede sobrescribir.

**Herramienta de ayuda:** [Generador de .htaccess de AyudaWP](https://herramientas.ayudawp.com/#htaccess)

### Forzar HTTPS

```apache
# Forzar HTTPS en todo el sitio
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
</IfModule>
```

### Activar compresión GZIP

Reduce el tamaño de los archivos que sirve tu servidor. El navegador los descomprime al vuelo.

```apache
# Compresión GZIP
<IfModule mod_deflate.c>
AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css
AddOutputFilterByType DEFLATE text/javascript application/javascript application/x-javascript
AddOutputFilterByType DEFLATE application/json application/ld+json
AddOutputFilterByType DEFLATE application/xml application/rss+xml
AddOutputFilterByType DEFLATE image/svg+xml
AddOutputFilterByType DEFLATE application/font-woff application/font-woff2
</IfModule>
```

### Caché del navegador

Le dice al navegador del visitante cuánto tiempo puede guardar cada tipo de archivo sin volver a pedirlo.

```apache
# Caché del navegador
<IfModule mod_expires.c>
ExpiresActive On
ExpiresDefault "access plus 1 month"
ExpiresByType text/html "access plus 1 hour"
ExpiresByType text/css "access plus 1 year"
ExpiresByType text/javascript "access plus 1 year"
ExpiresByType application/javascript "access plus 1 year"
ExpiresByType image/jpeg "access plus 1 year"
ExpiresByType image/png "access plus 1 year"
ExpiresByType image/webp "access plus 1 year"
ExpiresByType image/avif "access plus 1 year"
ExpiresByType image/svg+xml "access plus 1 year"
ExpiresByType application/font-woff "access plus 1 year"
ExpiresByType application/font-woff2 "access plus 1 year"
ExpiresByType image/x-icon "access plus 1 year"
</IfModule>
```

---

## Snippets PHP para functions.php o mu-plugins

Estos fragmentos puedes añadirlos al `functions.php` de tu tema hijo o, mejor aún, como un mu-plugin en `wp-content/mu-plugins/`. Si usas mu-plugins, crea un archivo PHP (por ejemplo `seo-tweaks.php`) y pega lo que necesites.

### Añadir extracto a las páginas

Por defecto WordPress solo permite extractos en las entradas. Activar extractos en páginas te da control sobre la meta description de cada una.

```php
// Activar extractos en páginas
add_post_type_support( 'page', 'excerpt' );
```

### Eliminar la categoría "Sin categoría" de los slugs

Si usas la estructura de permalinks con categoría, esto limpia las URLs de entradas sin categoría asignada.

```php
// Redirigir /sin-categoria/entrada/ a /entrada/
add_filter( 'post_link', function( $permalink, $post ) {
    if ( false !== strpos( $permalink, '%category%' ) ) {
        $cats = get_the_category( $post->ID );
        if ( $cats ) {
            $lowest_cat = $cats[0];
            // Buscar la categoría padre más baja en la jerarquía
            foreach ( $cats as $cat ) {
                if ( $cat->parent == 0 && $cat->slug === 'sin-categoria' ) {
                    continue;
                }
                $lowest_cat = $cat;
                break;
            }
            $permalink = str_replace( '%category%', $lowest_cat->slug, $permalink );
        }
    }
    return $permalink;
}, 10, 2 );
```

### Añadir meta description desde el extracto

Si no usas plugin de SEO, puedes generar automáticamente la meta description a partir del extracto de cada entrada o página.

```php
// Meta description automática desde el extracto
add_action( 'wp_head', function() {
    if ( is_singular() ) {
        global $post;
        $excerpt = $post->post_excerpt;
        if ( empty( $excerpt ) ) {
            $excerpt = wp_trim_words( wp_strip_all_tags( $post->post_content ), 25, '...' );
        }
        $excerpt = esc_attr( wp_strip_all_tags( $excerpt ) );
        if ( ! empty( $excerpt ) ) {
            echo '<meta name="description" content="' . $excerpt . '">' . "\n";
        }
    }
});
```

---

## Prompts optimizados para SEO y contenidos

Estos prompts siguen las técnicas de [prompt engineering del optimizador de AyudaWP](https://herramientas.ayudawp.com/#prompt-optimizer): rol específico, contexto claro, formato definido, restricciones explícitas, y técnicas avanzadas como chain of thought y few-shot donde aportan valor.

Copia el que necesites, adapta las variables entre `[corchetes]` a tu caso y pégalo en tu IA favorita.

### Redacción de artículos optimizados para SEO y GEO

```
Eres un redactor web especializado en SEO y GEO (Generative Engine Optimization) con 
más de 10 años de experiencia en contenidos para WordPress.

TAREA:
Escribe un artículo completo sobre [TEMA] optimizado tanto para buscadores como para 
IAs generativas (ChatGPT, Perplexity, Google AI Overviews).

CONTEXTO:
- Palabra clave principal: [PALABRA CLAVE]
- Palabras clave secundarias: [PALABRA 1, PALABRA 2, PALABRA 3]
- Audiencia: [DESCRIBE TU AUDIENCIA - ejemplo: propietarios de tiendas online 
  sin conocimientos técnicos]
- El artículo se publicará en un blog WordPress en español de España
- Competencia a superar: [URL DEL ARTÍCULO QUE QUIERES SUPERAR, si tienes uno]

FORMATO DE SALIDA:
- Tono: cercano y conversacional, de tú a tú, sin formalidades
- Estructura:
  * Título H1 con la palabra clave principal
  * Primer párrafo que responda directamente a la intención de búsqueda 
    (las IAs priorizan las respuestas directas al inicio)
  * Secciones con H2 y H3 en jerarquía lógica
  * Al menos una lista o tabla que las IAs puedan extraer fácilmente
  * Una sección de preguntas frecuentes al final (formato pregunta H3 + respuesta)
  * Conclusión con resumen accionable
- Extensión: 1.500-2.000 palabras
- Incluye sugerencia de meta description (máximo 155 caracteres)
- Incluye sugerencia de texto alternativo para la imagen destacada

RESTRICCIONES:
- No uses anglicismos innecesarios
- Evita frases vacías: "en este sentido", "cabe destacar", "sin lugar a dudas"
- Evita palabras típicas de IA: vibrante, holístico, epítome, inquebrantable
- No repitas la palabra clave de forma forzada, intégrala de forma natural
- Usa datos concretos (cifras, porcentajes, fechas) en lugar de generalidades
- Cita fuentes cuando menciones datos o estadísticas
- No uses emojis
```

### Descripciones de producto para WooCommerce

```
Eres un copywriter especializado en ecommerce y WooCommerce con amplia experiencia 
en SEO para tiendas online.

TAREA:
Escribe la descripción completa para un producto de WooCommerce optimizada para SEO, 
para IAs generativas, y para la conversión.

CONTEXTO:
- Producto: [NOMBRE DEL PRODUCTO]
- Categoría: [CATEGORÍA]
- Precio: [PRECIO]
- Características principales: [LISTA DE CARACTERÍSTICAS]
- Público objetivo: [A QUIÉN VA DIRIGIDO]
- Ventaja competitiva: [QUÉ LO DIFERENCIA DE LA COMPETENCIA]
- Tienda en WordPress/WooCommerce, contenido en español de España

FORMATO DE SALIDA:
Genera estos 4 elementos por separado y bien diferenciados:

1. DESCRIPCIÓN CORTA (para el extracto de WooCommerce):
   - Máximo 2-3 frases
   - Incluir la palabra clave principal y el beneficio principal
   - Debe funcionar como gancho, lo primero que lee el cliente

2. DESCRIPCIÓN LARGA (para la pestaña de descripción):
   - Primer párrafo: respuesta directa a "qué es y para quién"
   - Sección de beneficios (no características, beneficios para el usuario)
   - Sección de especificaciones técnicas en formato tabla
   - Sección de preguntas frecuentes (2-3 preguntas habituales del comprador)
   - Extensión: 300-500 palabras

3. META DESCRIPTION: máximo 155 caracteres, con palabra clave y llamada a la acción

4. TEXTO ALTERNATIVO para la imagen principal del producto

RESTRICCIONES:
- Tono: directo, cercano, enfocado en beneficios
- Sin superlativos vacíos: "el mejor", "increíble", "revolucionario"
- Las especificaciones técnicas siempre en tabla, las IAs las extraen mejor
- No uses emojis
- Incluye datos concretos: medidas, pesos, materiales, compatibilidades
```

### Lote de meta descriptions

```
Eres un especialista SEO con experiencia en redacción de meta descriptions que 
maximizan el CTR en los resultados de búsqueda.

TAREA:
Genera meta descriptions optimizadas para las siguientes URLs/páginas de mi sitio 
WordPress.

CONTEXTO:
- Sitio web: [TU DOMINIO]
- Sector: [TU SECTOR]
- Páginas a optimizar:
  1. [URL o TÍTULO DE LA PÁGINA 1] — palabra clave: [KEYWORD 1]
  2. [URL o TÍTULO DE LA PÁGINA 2] — palabra clave: [KEYWORD 2]
  3. [URL o TÍTULO DE LA PÁGINA 3] — palabra clave: [KEYWORD 3]
  [añade tantas como necesites]

FORMATO DE SALIDA:
Para cada página genera exactamente:
- Meta description: máximo 155 caracteres (cuenta los caracteres)
- Incluir la palabra clave de forma natural
- Incluir una llamada a la acción implícita o explícita
- Que funcione como "gancho" para que el usuario haga clic

EJEMPLO DE LO QUE ESPERO:
Entrada: "Guía de optimización WPO en WordPress" — keyword: "optimización WordPress"
Salida: "Aprende a optimizar tu WordPress paso a paso con técnicas WPO probadas. 
Mejora la velocidad de tu web sin plugins de pago ni conocimientos técnicos." 
(154 caracteres)

RESTRICCIONES:
- Cuenta los caracteres de cada meta description y muéstralos entre paréntesis
- No superes los 155 caracteres en ningún caso
- No empieces todas con el mismo patrón (varía entre pregunta, afirmación, dato)
- No uses emojis
- Español de España
```

### Estructura de contenidos para posicionar en AI Overviews

```
Eres un consultor de GEO (Generative Engine Optimization) especializado en conseguir 
que los contenidos aparezcan en las respuestas de IAs generativas como Google AI 
Overviews, ChatGPT y Perplexity.

TAREA:
Analiza la intención de búsqueda de la siguiente consulta y genera un esquema de 
contenido optimizado para aparecer en las respuestas de las IAs generativas.

CONSULTA OBJETIVO: [ESCRIBE AQUÍ LA BÚSQUEDA QUE QUIERES ATACAR]

CONTEXTO:
- El contenido se publicará en WordPress
- Audiencia: [DESCRIBE TU AUDIENCIA]
- Idioma: español de España
- Las IAs generativas priorizan contenidos con: respuestas directas al inicio, 
  datos estructurados, formato pregunta-respuesta, listas y tablas extraíbles, 
  fuentes citadas, y autoridad demostrada en el tema

FORMATO DE SALIDA:
Piensa paso a paso y genera:

1. ANÁLISIS DE INTENCIÓN:
   - ¿Qué busca realmente el usuario con esta consulta?
   - ¿Qué tipo de respuesta esperan las IAs? (lista, explicación, comparativa, 
     guía paso a paso, definición)

2. ESQUEMA DE CONTENIDO OPTIMIZADO PARA GEO:
   - Título H1 propuesto
   - Primer párrafo (la "respuesta directa" que las IAs pueden extraer, 
     2-3 frases máximo)
   - Estructura de H2 y H3
   - Indica dónde incluir tablas y listas
   - Indica dónde incluir bloques de pregunta-respuesta
   - Indica dónde incluir datos concretos y fuentes

3. SNIPPET OBJETIVO:
   - Redacta el fragmento de texto (máximo 50 palabras) que querrías que una IA 
     extrajera y citara como respuesta

RESTRICCIONES:
- No generes el artículo completo, solo el esquema y el snippet
- El esquema debe ser accionable: que cualquiera pueda escribir el artículo 
  siguiéndolo
- Prioriza la estructura que mejor funcione para la intención detectada
```

### Auditoría SEO técnica con IA

```
Eres un consultor SEO técnico senior especializado en WordPress con más de 10 años 
de experiencia en auditorías de rendimiento y rastreo.

TAREA:
Realiza una auditoría SEO técnica del siguiente sitio WordPress y genera un informe 
con problemas detectados y soluciones específicas.

CONTEXTO:
- URL del sitio: [TU URL]
- Hosting: [TU HOSTING - ejemplo: SiteGround, hosting compartido genérico, VPS...]
- Tema activo: [NOMBRE DEL TEMA]
- Plugins SEO instalados: [NINGUNO / lista de plugins si los hay]
- Plugins de caché: [NINGUNO / lista si los hay]
- Problemas que he detectado: [DESCRIBE LO QUE HAS NOTADO - ejemplo: carga lenta, 
  caída de posiciones, páginas no indexadas...]
- Accedo al servidor vía: [cPanel / SSH / solo el panel de WordPress]

FORMATO DE SALIDA:
Organiza el informe en estas secciones, ordenando los problemas de mayor a menor 
impacto:

1. RASTREO E INDEXACIÓN
   - Estado del robots.txt
   - Estado del sitemap XML
   - Páginas que no deberían indexarse
   - Problemas de crawl budget

2. RENDIMIENTO
   - TTFB estimado y recomendaciones
   - Recursos que bloquean el renderizado
   - Compresión y caché
   - Core Web Vitals

3. CONTENIDO Y ESTRUCTURA
   - Problemas de encabezados
   - Meta descriptions ausentes o duplicadas
   - Contenido duplicado o thin content
   - Enlazado interno

4. PREPARACIÓN PARA IA (GEO)
   - Datos estructurados / JSON-LD
   - Disponibilidad de llms.txt
   - Accesibilidad para bots de IA

Para cada problema incluye:
- Qué es y por qué afecta al SEO
- Cómo solucionarlo (comando, snippet o paso concreto)
- Prioridad: alta / media / baja

RESTRICCIONES:
- Soluciones compatibles con WordPress sin plugins de SEO (o con plugins gratuitos)
- Código compatible desde PHP 7.4
- Si recomiendas tocar archivos del servidor, indica siempre hacer copia de seguridad
- No recomiendes plugins de pago sin dar alternativa gratuita
```

### Textos para páginas de categoría y taxonomías

```
Eres un redactor SEO especializado en arquitectura de contenidos para WordPress 
y WooCommerce.

TAREA:
Redacta textos optimizados para las páginas de categoría/taxonomía de mi sitio 
WordPress que actualmente están vacías o con descripciones genéricas.

CONTEXTO:
- Tipo de sitio: [blog / tienda WooCommerce / web corporativa]
- Sector: [TU SECTOR]
- Categorías a optimizar:
  1. [NOMBRE DE CATEGORÍA 1] — keyword: [KEYWORD]
  2. [NOMBRE DE CATEGORÍA 2] — keyword: [KEYWORD]
  3. [NOMBRE DE CATEGORÍA 3] — keyword: [KEYWORD]

FORMATO DE SALIDA:
Para cada categoría genera:

1. DESCRIPCIÓN DE CATEGORÍA (la que va en WordPress como descripción de la 
   taxonomía):
   - 2-3 párrafos (150-250 palabras)
   - Primer párrafo: definición clara de qué encontrará el usuario en esta categoría
   - Segundo párrafo: contexto útil, por qué es relevante, qué problemas resuelve
   - Tercer párrafo (opcional): enlace natural a categorías relacionadas
   - Incluir la keyword de forma natural

2. META DESCRIPTION: máximo 155 caracteres

RESTRICCIONES:
- Tono cercano, conversacional
- No rellenes con texto vacío para hacer bulto
- Cada descripción debe aportar valor real al usuario que llega a esa categoría
- No repitas la misma estructura en todas, varía el enfoque
- Español de España, sin emojis
```

### Prompt para generar FAQs estructuradas

```
Eres un especialista en SEO y datos estructurados con experiencia en conseguir 
resultados enriquecidos en Google y respuestas en IAs generativas.

TAREA:
Genera un bloque de preguntas frecuentes (FAQ) sobre [TEMA] optimizado para:
- Aparecer como resultado enriquecido en Google (FAQ schema)
- Ser extraído por IAs generativas como fuente de respuestas

CONTEXTO:
- El FAQ se añadirá a la entrada/página: [URL o TÍTULO]
- Audiencia: [DESCRIBE TU AUDIENCIA]
- El sitio usa WordPress con el editor de bloques

FORMATO DE SALIDA:
- Entre 5 y 8 preguntas
- Cada pregunta como H3
- Cada respuesta: primer párrafo con la respuesta directa (máximo 2-3 frases), 
  segundo párrafo con información adicional si es necesario
- Las respuestas deben ser autónomas: que se entiendan sin leer el resto del artículo
- Incluir al menos una respuesta con lista y una con dato concreto (cifra, fecha, 
  porcentaje)

EJEMPLO DE LO QUE ESPERO:

### ¿Cuántas revisiones guarda WordPress por defecto?

WordPress guarda todas las revisiones de cada entrada sin límite. Esto significa 
que si editas una entrada 50 veces, tendrás 50 copias en la base de datos.

Puedes limitar el número de revisiones añadiendo 
`define('WP_POST_REVISIONS', 5);` en tu archivo wp-config.php. Un valor entre 
3 y 5 revisiones suele ser suficiente para la mayoría de sitios.

RESTRICCIONES:
- Preguntas reales que haría tu audiencia, no preguntas forzadas para meter keywords
- Respuestas concisas, sin rodeos
- No empieces todas las respuestas con "Sí, ..." o "No, ..."
- Español de España, sin emojis
```

---

## Lecturas recomendadas

- [SEO e IA: todo lo que necesitas saber](https://ayudawp.com/seo-ia/)
- [El gran desacoplamiento de Google](https://ayudawp.com/gran-desacoplamiento-google/)
- [AI Overviews de Google](https://ayudawp.com/ai-overviews-google/)
- [Todo sobre llms.txt y llms-full.txt](https://ayudawp.com/llms-txt-llms-full-txt/)
- [Markdown para agentes IA](https://ayudawp.com/markdown-agentes-ia/)
- [JSON-LD en WordPress](https://ayudawp.com/json-ld/)
- [Todo sobre el TTFB](https://ayudawp.com/ttfb/)
- [Prompts para WordPress e IA](https://ayudawp.com/prompts-ia-wordpress/)
- [Descripciones de WooCommerce con IA](https://ayudawp.com/descripciones-woocommerce-ia/)
- [Productos de WooCommerce en ChatGPT](https://ayudawp.com/productos-woocommerce-chatgpt/)
- [Recomendaciones de IA para tu tienda](https://ayudawp.com/recomendaciones-ia/)

---

*Todos los plugins, herramientas y prompts mencionados son 100% gratuitos.*

*Genera tus prompts optimizados con el [Optimizador de prompts de AyudaWP](https://herramientas.ayudawp.com/#prompt-optimizer)*

*¿Te ha sido útil? Visita [AyudaWP.com](https://ayudawp.com) para más recursos sobre WordPress.*
