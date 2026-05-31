# 🍄 Gran Espíritu — Catálogo Digital

> Catálogo de productos para **Gran Espíritu**, marca chilena de medicina fungi natural
> (hongos medicinales + adaptógenos ayurvédicos). Pensado para móvil, con carrito de
> compras y pedidos por WhatsApp.

**Entregado por:** nico.agenteia · **Fecha:** Mayo 2026
**Instagram:** [@granespiri.tu.official](https://www.instagram.com/granespiri.tu.official)

---

## 1. ¿Qué es este proyecto?

Es una **tienda / catálogo digital** que funciona en un solo archivo HTML. El cliente
puede:

- Ver todos los productos organizados por categoría
- Ver las **promociones** (packs combinados con descuento)
- Buscar productos y filtrarlos
- Agregar productos a un carrito
- Finalizar el pedido eligiendo método de pago (Transferencia / Efectivo / Tarjeta)
- Coordinar todo por **WhatsApp** con un mensaje que se arma solo

No necesita base de datos, ni servidor, ni cuenta de programador para funcionar. Se abre
como una página web normal y ya está listo.

---

## 2. Cómo abrirlo y probarlo

### Opción rápida (en el computador)
Hacer **doble clic** en el archivo `gran-espiritu-catalogo.html`. Se abre en el navegador
(Chrome, Edge, etc.) y funciona completo.

> ⚠️ Importante: para que se vean las imágenes, el archivo `gran-espiritu-catalogo.html`
> siempre debe estar **junto a las carpetas `img/` y `fotos/`**. No mover el HTML solo.

### Cómo se ve mejor
Está diseñado para **celular** (formato vertical). En el computador se ve centrado, como
si fuera la pantalla de un teléfono. Eso es intencional.

---

## 3. Estructura de archivos

```
GRAN-ESPIRITU/
├── gran-espiritu-catalogo.html   ← LA TIENDA (todo el código está aquí)
├── DOCUMENTACION.md              ← este documento
│
├── img/                          ← imágenes que SE USAN en la tienda
│   ├── hero-bosque1.jpg          (fotos de producto del catálogo)
│   ├── reishi.jpg
│   ├── cordyceps.jpg
│   ├── ... (18 imágenes de producto)
│   │
│   └── promos/                   ← imágenes de las 9 promociones
│       ├── promo-flash.jpg
│       ├── promo-zen.jpg
│       ├── promo-cuarteto-fungi.jpg
│       └── ... (9 promos)
│
└── fotos/                        ← material original del cliente (19 fotos sin editar)
    ├── logo.png
    └── IMG-...WA....jpg           (fotos de respaldo / banco de imágenes)
```

- **`img/`** → son las imágenes que la tienda muestra. Si cambias una foto aquí, cambia en
  la tienda.
- **`img/promos/`** → las 9 imágenes de promociones (diseñadas con todo el texto y precio
  adentro).
- **`fotos/`** → banco de fotos originales del cliente (WhatsApp). No se muestran
  directamente; sirven de reserva para futuras ediciones.

---

## 4. Cómo poner la tienda en internet (publicarla)

Hoy funciona abriendo el archivo. Para que tenga un **link compartible** (ej.
`granespiritu.cl`), hay que subirla a un hosting. Opciones recomendadas (todas con plan
gratis):

| Servicio | Cómo | Ideal para |
|----------|------|------------|
| **Netlify** | Arrastrar la carpeta completa a netlify.com/drop | Lo más fácil, 2 minutos |
| **Vercel** | Subir la carpeta | Rápido y profesional |
| **GitHub Pages** | Subir a un repositorio | Si ya usas GitHub |

> 💡 **Recomendación:** al publicar, renombrar `gran-espiritu-catalogo.html` a
> **`index.html`**. Así el link queda limpio (`tudominio.cl` en vez de
> `tudominio.cl/gran-espiritu-catalogo.html`).

Después se puede conectar un dominio propio (ej. `.cl`) desde el mismo panel del hosting.

---

## 5. Guía de edición (lo más importante)

Todo el contenido editable está dentro del archivo `gran-espiritu-catalogo.html`. Para
editarlo se abre con cualquier editor de texto (Bloc de notas, o mejor **VS Code**) y se
usa **Buscar** (`Ctrl + F`) para encontrar cada sección.

### 5.1 Cambiar el número de WhatsApp
Buscar: `WA_NUMBER`

```js
const WA_NUMBER = '56947857304'; // ← cambiar aquí (formato: 56 + número sin +)
```

> El número aparece también en el botón flotante y el footer. Si cambia, buscar
> `56947857304` en todo el archivo y reemplazar todas las apariciones.

### 5.2 Editar, agregar o quitar PRODUCTOS
Buscar: `PRODUCTS_DATA`

Cada producto es un bloque así:

```js
{
  id: 1,                                    // número único (no repetir)
  nombre: "Melena de León · Tintura",
  nombreCientifico: "Hericium erinaceus",
  categoria: "Foco",                        // ver categorías válidas abajo
  marca: "Gran Espíritu",
  beneficio: "Neuroprotección & Foco",      // texto verde sobre el nombre
  descripcion: "Tintura de extracto doble...",
  precio: 14990,                            // precio actual (sin puntos)
  precioNormal: 18990,                      // precio antes (tachado). null si no hay oferta
  precioUnidad: "30ml · Extracto 1:3",
  imagen: "./img/hero-bosque1.jpg",         // ruta de la foto
  stock: true,                              // false = "Agotado"
  promo: "Más vendido",                     // etiqueta esquina. null si no tiene
  unidadesRestantes: null                   // ej: 5 muestra "Últimas 5 unidades". null = nada
},
```

**Para agregar un producto:** copiar un bloque completo, pegarlo, cambiar los datos y
ponerle un `id` nuevo.
**Para quitar uno:** borrar el bloque entero (desde `{` hasta `},`).

**Categorías válidas** (deben escribirse igual): `Hongos`, `Energía`, `Foco`, `Calma`,
`Inmunidad`, `Adaptógenos`, `Cuidado`.

### 5.3 Editar, agregar o quitar PROMOCIONES
Buscar: `PROMOS_DATA`

Las promociones salen en el **carrusel de arriba** y en la **sección "🔥 Promociones"**.
Cada una es así:

```js
{
  id: 'flash',                              // identificador único en texto
  nombre: 'Promo Flash',
  tag: 'Tu dúo de bienestar a elección',    // frase corta bajo el nombre
  img: './img/promos/promo-flash.jpg',      // imagen de la promo
  incluye: [                                // qué trae (sale en el mensaje de WhatsApp)
    '1 Triple extracto de hongo a elección',
    '1 frasco de 30 cápsulas (hongo o planta)'
  ],
  precio: 19990,                            // precio promo
  precioRef: 26980                          // precio de referencia (tachado). Calcula el % ahorro solo
},
```

El **% de ahorro** ("Ahorra 26%") se calcula automáticamente con `precio` y `precioRef`.

> Para que una promo nueva se vea, su imagen debe estar en la carpeta `img/promos/`.

### 5.4 Cambiar los datos bancarios (transferencia)
Buscar: `Datos para transferencia`

```html
<span class="tr-value">Banco Estado</span>
<span class="tr-value">Cuenta Corriente</span>
<span class="tr-value">0123456789</span>      ← N° de cuenta
<span class="tr-value">12.345.678-9</span>    ← RUT
<span class="tr-value">Gran Espíritu</span>   ← Nombre
```

> ⚠️ **Estos datos son de ejemplo. Hay que reemplazarlos por los reales antes de publicar.**

### 5.5 Cambiar el Instagram / redes
Buscar: `instagram.com` — está en el footer (pie de página).

### 5.6 Cambiar imágenes
- Guardar la nueva imagen en `img/` (o `img/promos/`).
- En el código, apuntar a ella: `imagen: "./img/mi-nueva-foto.jpg"`.
- **Formato ideal:** imágenes **cuadradas** (1:1), JPG, livianas (menos de 300 KB para que
  cargue rápido).

---

## 6. Funcionalidades incluidas

- ✅ **Carrusel de promociones** con auto-avance, flechas y deslizar con el dedo
- ✅ **Buscador** de productos en tiempo real
- ✅ **Filtro por categoría** (pills arriba + hub de íconos)
- ✅ **Ordenar** por relevancia, precio o descuento
- ✅ **Carrito** con sumar/restar cantidad, subtotal y nota del pedido
- ✅ **Checkout** con 3 métodos: Transferencia, Efectivo, Tarjeta
- ✅ **Pedido por WhatsApp** con el mensaje armado automáticamente
- ✅ **Botón flotante de WhatsApp** siempre visible
- ✅ Diseño responsive, animaciones suaves, badges de stock y "últimas unidades"
- ✅ Optimizado para compartir en redes (vista previa con imagen y descripción)

---

## 7. ¿Cómo llega un pedido?

1. El cliente agrega productos al carrito.
2. Presiona **"Proceder al pago"** y elige cómo pagar.
3. Al confirmar, se abre **WhatsApp** con un mensaje ya escrito (productos, cantidades y
   total) hacia el número del negocio.
4. El negocio recibe el mensaje y **coordina disponibilidad, pago y entrega** por chat.

> El catálogo **no cobra automáticamente**: es una herramienta para generar el pedido y
> llevar la conversación a WhatsApp, que es donde se cierra la venta.

---

## 8. ⚠️ Nota importante sobre el pago con Tarjeta (Webpay)

El paso **"Tarjeta (Webpay Plus)"** es actualmente una **simulación / demostración
visual**: se ve como un pago real, pero **no procesa cobros** ni se conecta a Transbank.
Los datos de tarjeta que se ingresan **no se envían a ningún lado** (no se guardan ni
viajan por internet).

**Antes de publicar, hay que decidir una de estas opciones:**

- **(A) Quitar el método Tarjeta** y dejar solo Transferencia + Efectivo + WhatsApp
  (lo más simple y honesto para empezar).
- **(B) Integrar una pasarela de pago real** (Webpay/Transbank, Mercado Pago o Flow) para
  cobrar de verdad con tarjeta. Esto requiere una cuenta del proveedor y un desarrollo
  adicional.

> Recomendación: empezar con la opción (A) y, cuando el volumen lo justifique, pasar a (B).

---

## 9. ✅ Checklist antes de publicar

- [ ] Reemplazar los **datos bancarios** de ejemplo por los reales (ver 5.4)
- [ ] Decidir qué hacer con el **pago con tarjeta** (ver sección 8)
- [ ] Revisar **precios y stock** de todos los productos
- [ ] Confirmar que el **número de WhatsApp** es el correcto
- [ ] (Opcional) Renombrar el HTML a `index.html` y subir a un hosting
- [ ] (Opcional) Conectar un dominio propio

---

## 10. Detalles técnicos (para quien mantenga el código)

- **Stack:** HTML + CSS + JavaScript puro (vanilla). **Sin frameworks ni dependencias** que
  instalar.
- **Tipografías:** Google Fonts — *DM Sans* (texto) y *Fraunces* (títulos).
- **Todo en un archivo:** estructura, estilos y lógica viven en
  `gran-espiritu-catalogo.html`. Fácil de mover y respaldar.
- **Datos:** los productos (`PRODUCTS_DATA`) y promociones (`PROMOS_DATA`) están como
  arreglos JavaScript dentro del archivo. El código está preparado para, en el futuro,
  cargar los datos desde un archivo externo (`productos.json`) o un sistema automatizado
  (n8n) sin rehacer la tienda.
- **Paleta:** estética "bosque húmedo" — pergamino `#f2ede6`, verde musgo `#3d5a40`,
  marrón hongo `#7a4e2d`.
- **Compatibilidad:** funciona en navegadores modernos (Chrome, Edge, Safari, Firefox) en
  celular y escritorio.

---

## 11. Resumen del catálogo actual

- **18 productos** en 7 categorías (hongos medicinales en tintura/cápsulas, adaptógenos
  ayurvédicos y cuidado personal).
- **9 promociones** (packs combinados): Flash, Zen, Vigorosidad, Cuarteto Fungi, Sinergia
  Ayurveda, Elixir de la Juventud, Potencia Tu Pack, Los 4 Fantásticos y Sexteto Fungi.

---

*Desarrollado con IA · **nico.agenteia** · Para Gran Espíritu 🍄*
