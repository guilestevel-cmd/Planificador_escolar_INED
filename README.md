# Planea — plan de actividades por unidad

Sitio estático (HTML, CSS y JavaScript puro) que usa un Google Sheet como
base de datos compartida a través de una pequeña API hecha en Apps Script.

## Paso 1 — Crear la base de datos (Google Sheets + Apps Script)

1. Ve a [sheets.new](https://sheets.new) y crea una hoja de cálculo nueva.
   Puede quedarse vacía; la aplicación crea las pestañas que necesita sola.
2. Extensiones → Apps Script.
3. Borra todo el contenido del archivo `Code.gs` que se abre y pega ahí el
   contenido del archivo `Code.gs` de esta carpeta.
4. Guarda (el ícono de disquete).
5. Implementar → Nueva implementación.
   - Tipo: **Aplicación web**.
   - Descripción: la que quieras (ej. "API Planea").
   - Ejecutar como: **Yo**.
   - Quién tiene acceso: **Cualquier usuario**.
6. Haz clic en Implementar. Google pedirá que autorices el script la
   primera vez — es normal, es tu propio script accediendo a tu propia hoja.
7. Copia la **URL de la aplicación web** que te da (termina en `/exec`).
   La necesitas en el paso 3.

Cada vez que cambies algo en `Code.gs`, tienes que volver a
**Implementar → Gestionar implementaciones → editar (lápiz) → Nueva versión**
para que el cambio quede activo en la URL.

## Paso 2 — Subir el sitio a GitHub

1. En GitHub, crea un repositorio nuevo (puede ser público o privado si
   tienes plan que lo permita para Pages).
2. Sube estos archivos a la raíz del repositorio: `index.html`,
   `styles.css`, `app.js`. (`Code.gs` y este `README.md` no son necesarios
   en GitHub, son solo de referencia — pero no pasa nada si los subes también.)
3. Ve a **Settings → Pages**.
4. En "Build and deployment", elige **Deploy from a branch**, rama `main`
   (o `master`), carpeta `/ (root)`. Guarda.
5. Espera uno o dos minutos y GitHub te dará una URL como
   `https://tu-usuario.github.io/tu-repositorio/`.

## Paso 3 — Conectar el sitio con la base de datos

1. Abre `app.js` (puedes editarlo directamente en GitHub, con el lápiz).
2. Al inicio del archivo, reemplaza:
   ```js
   const URL_API = 'PON_AQUI_LA_URL_DE_TU_APLICACION_WEB_DE_APPS_SCRIPT';
   ```
   con la URL que copiaste en el paso 1.7.
3. Guarda (commit). GitHub Pages se actualiza solo en uno o dos minutos.

Listo — entra a la URL de GitHub Pages y ya debería cargar el planeador,
compartiendo datos entre todas las personas que lo usen.

## Notas

- El rol (Administración / Comisión / Profesor) se guarda en el navegador
  de cada persona, no es una contraseña — cualquiera con el enlace puede
  elegir cualquier rol. Si más adelante necesitas que sea privado de
  verdad, se puede agregar una clave de acceso simple o usar el sistema
  de cuentas de Google.
- Todos los datos (unidades y actividades) viven en las pestañas
  "Unidades", "Actividades" y "Configuracion" de tu Google Sheet — puedes
  abrirlas directamente para revisar o corregir algo a mano si hace falta.
- El botón "Imprimir / descargar PDF" del reporte usa el diálogo de
  impresión del navegador; ahí se elige "Guardar como PDF".
