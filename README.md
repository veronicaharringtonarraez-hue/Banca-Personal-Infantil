# Banco Crece 🪙 — Banca Personal Infantil

App para enseñar economía a los niños (Taylor, Emmeth y Christopher): ganar dinero
con tareas, pagar gastos, ahorrar para una meta, diezmo, presupuesto y logros.

## Instalar como app "ChildBank" (ícono en el Escritorio)

La app es **instalable**. Una vez abierta la dirección en internet:

- **Computadora (Chrome/Edge):** aparece un ícono de instalar ⊕ en la barra de
  direcciones, o ve al menú **⋮ → Guardar y compartir → Instalar / Crear acceso
  directo** (marca "Abrir como ventana"). Se crea el ícono **ChildBank** en el
  Escritorio.
- **iPhone/iPad (Safari):** botón **Compartir → Añadir a pantalla de inicio**.
- **Android (Chrome):** menú **⋮ → Instalar aplicación / Añadir a pantalla de inicio**.

El ícono se toma de `icons/childbank-512.png`. Si quieres cambiarlo, reemplaza
ese archivo (PNG 512×512).

## ¿Dónde se guardan los datos?

Todo se guarda **automáticamente en el navegador** (almacenamiento local del
dispositivo). Cada vez que abras la app en el **mismo navegador** verás tus
saldos, pagos, ahorros y presupuestos tal como los dejaste, mes a mes. No hace
falta ningún botón de "guardar": los cambios quedan solos.

> Importante: los datos viven en el navegador donde la usas. Si abres la app en
> otro teléfono o computadora, ese dispositivo empieza limpio.

### Respaldo y pasar datos a otro dispositivo

En **Modo Mamá/Papá → 💾 Respaldo de datos**:

- **⬇️ Descargar respaldo:** guarda un archivo con toda la información.
- **⬆️ Restaurar desde un archivo:** carga ese archivo en otro dispositivo (o
  para recuperar datos). Reemplaza lo que haya en ese navegador.

Es buena idea descargar un respaldo de vez en cuando para no perder nada.

## Cómo usarla en internet (GitHub Pages)

La app ya está lista para publicarse gratis con una dirección web. Para activarla
una sola vez:

1. En GitHub entra a tu repositorio → pestaña **Settings** (Configuración).
2. En el menú de la izquierda, abre **Pages**.
3. En **Build and deployment → Source**, elige **GitHub Actions**.
4. Listo. Cada vez que se actualice la rama principal (`main`), se publica sola.
   La dirección aparece en **Settings → Pages** (algo como
   `https://veronicaharringtonarraez-hue.github.io/Banca-Personal-Infantil/`).

Abre esa dirección en el teléfono o computadora y guárdala en favoritos o en la
pantalla de inicio.

## Cómo editar los presupuestos mes a mes

1. Abre la app y toca el botón **👩‍👧‍👦 Mamá/Papá** (arriba a la derecha).
2. Ingresa el PIN (por defecto **181215**, lo puedes cambiar ahí mismo).
3. Elige al niño con las pestañas de arriba.
4. En la tarjeta **📊 Presupuesto de [niño]** cambia el monto de cada gasto
   (Alquiler, Alimentación, etc.). Se guarda solo al salir del campo.
5. Botón **↩️ Restablecer montos por defecto** vuelve a los valores originales de
   ese mes.

Cada mes nuevo arranca usando estos valores como base, y puedes ajustarlos otra
vez cuando quieras. También puedes dar puntos, registrar el bono de exámenes y
cambiar la meta de ahorro desde el mismo Modo Mamá/Papá.

## Estructura del proyecto

- `index.html` — página principal (carga React + Babel desde internet).
- `app/data.js` — configuración: niños, gastos por defecto, tareas, logros.
- `app/store.jsx` — estado y guardado en el navegador (incluye presupuestos editables).
- `app/screens.jsx` — pantallas del niño (Inicio, Ganar, Pagar, Ahorro, etc.).
- `app/parent.jsx` — Modo Mamá/Papá (editor de presupuesto, puntos, metas, PIN).
- `app/components.jsx`, `app/app.jsx`, `app/tweaks-panel.jsx` — piezas de apoyo.
- `.github/workflows/pages.yml` — publica la app en GitHub Pages automáticamente.

## Probarla en tu computadora (opcional)

Como usa archivos `.jsx`, ábrela con un servidor local (no con doble clic):

```bash
python3 -m http.server 8000
# luego abre http://localhost:8000 en el navegador
```
