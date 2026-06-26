# 🔐 Panel de Administración — UPGRADE (desactivado)

> **Estado actual:** DESACTIVADO. El catálogo funciona con precios y datos
> locales (hardcoded en `index.html`). Este documento explica cómo reactivar el
> panel de administración cuando el cliente contrate el upgrade.

---

## ¿Qué es este upgrade?

Un panel de administración que permite al cliente, **sin tocar código**:

- Editar precio, precio de referencia y stock de cada producto
- Editar nombre, descripción corta, descripción expandida, beneficio y categoría
- Cambiar la foto de cada producto (subiéndola desde el celular)
- Agregar productos nuevos
- Los cambios se guardan en una base de datos (Supabase) y se reflejan en el sitio

Acceso pensado: enlace discreto en el footer → login con contraseña → panel.

---

## Cómo reactivarlo (3 pasos)

Todo el código ya está construido y presente en `index.html`. Solo está
desactivado mediante una bandera. Para reactivar:

### 1. Activar la bandera en el script
En `index.html`, busca:
```js
const ADMIN_ENABLED = false;
```
Cámbialo a:
```js
const ADMIN_ENABLED = true;
```
Esto reactiva: la carga de datos desde Supabase en `fetchData()` y el acceso al
panel vía `#admin`.

### 2. Mostrar el enlace de acceso en el footer
En `index.html`, busca el bloque comentado `UPGRADE Panel Admin (desactivado)`
(dentro de `<div class="footer-credit">`) y descomenta la línea del enlace:
```html
<a href="#admin" class="footer-credit-link" style="...">🔐 Administrar catálogo</a>
```

### 3. Hacer commit y push
```bash
git add index.html
git commit -m "feat: reactivar panel admin (upgrade contratado)"
git push
```
Vercel desplegará automáticamente. Listo.

---

## Acceso al panel

- **URL:** `https://<sitio>.vercel.app/#admin` (o el enlace del footer)
- **Contraseña:** `granespiritu2026`
  - Definida en `index.html` → `const ADMIN_PASS = 'granespiritu2026';`
  - Conviene cambiarla por una más fuerte al entregar.

---

## Infraestructura ya creada (Supabase)

> ⚠️ El proyecto Supabase es **compartido con el proyecto Smile** (verduras/frutas).
> Gran Espíritu usa solo objetos con prefijo `ge_`. **No tocar nada sin ese prefijo.**

- **Proyecto:** `qovlxtenzpwwtwhrbqip`
- **URL:** `https://qovlxtenzpwwtwhrbqip.supabase.co`
- **API key (anon, pública):** ya embebida en `index.html` (`SB_KEY`)

### Tablas
- **`ge_productos`** — datos completos editables de los 19 productos
  (product_id, nombre, descripcion, descripcion_extra, imagen, precio,
  precio_normal, precio_unidad, beneficio, categoria, stock, promo, updated_at).
  Ya tiene los 19 productos cargados.
- **`ge_precios`** — tabla previa (solo precio/stock). Quedó obsoleta; `ge_productos`
  la reemplaza. Puede ignorarse o borrarse en el futuro.

RLS: lectura pública + escritura con anon key (ambas tablas).

### Storage
- **Bucket `ge-imagenes`** (público) — para las fotos que el cliente suba desde
  el panel. Políticas: lectura pública, subida/edición con anon key.

---

## Funcionamiento técnico (referencia)

Funciones clave en `index.html` (todas presentes, gateadas por `ADMIN_ENABLED`):

- `sbFetch(path, opts)` — helper REST a Supabase.
- `fetchData()` — si `ADMIN_ENABLED`, sobreescribe `PRODUCTS_DATA` con lo de
  `ge_productos`; si no, usa los datos locales (comportamiento actual).
- `checkAdmin()` / `openAdminLogin()` / `adminLogin()` — acceso y login.
- `renderAdminPanel()` — UI del panel (cards expandibles por producto).
- `uploadAdminImg()` — comprime (max 800px, JPEG 0.8) y sube a `ge-imagenes`.
- `addNewProduct()` — agrega producto nuevo en el panel.
- `saveAdmin()` — guarda (PATCH/POST) a `ge_productos`.

CSS del panel: clases `.admin-*` (panel como página completa).

---

## Verificación tras reactivar

1. Abrir `/#admin` → aparece login → ingresar contraseña → se ve el panel con los
   19 productos.
2. Cambiar un precio → "Guardar todo" → recargar el sitio → el precio nuevo se ve.
3. Subir una foto a un producto → guardar → la foto nueva aparece en el catálogo.
4. Si Supabase no responde, el sitio sigue funcionando con los datos locales (fallback).

---

*Documentado por nico.agenteia — upgrade listo para activar cuando se contrate.*
