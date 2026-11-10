# Control de barrenación larga · COMINVI

App web (también instalable en el celular) para registrar y consultar el avance de barrenación larga por rebaje.
Los datos se guardan en **Firebase Firestore**, así que todos ven lo mismo en tiempo real.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La app completa |
| `config.js` | Datos de Firebase y huella de la clave de editor (lo editas tú) |
| `datos_migracion.json` | Respaldo de la app anterior, para importarlo una sola vez |
| `firestore.rules` | Reglas de seguridad para pegar en Firebase |
| `manifest.webmanifest`, `icon.svg` | Ícono y nombre al instalarla en el celular |

## 1. Crear la base de datos (Firebase, gratis)

1. Entra a https://console.firebase.google.com con tu cuenta de Google y crea un proyecto (por ejemplo `barrenacion-cominvi`). Puedes desactivar Google Analytics.
2. En el menú **Compilación > Firestore Database**, pulsa **Crear base de datos**, ubicación `us-central` (o la más cercana) y modo **producción**.
3. En la pestaña **Reglas**, borra lo que hay, pega el contenido de `firestore.rules` y pulsa **Publicar**.
4. Ve a **Configuración del proyecto** (engrane) > **Tus apps** > ícono `</>` (Web). Ponle un nombre y regístrala (no actives Hosting).
5. Copia los valores de `firebaseConfig` (apiKey, authDomain, projectId, storageBucket, messagingSenderId, appId) y pégalos en `config.js` en lugar de cada `PEGA_AQUI`.

## 2. Publicar en GitHub Pages

1. En GitHub crea un repositorio nuevo, por ejemplo `barrenacion-larga` (público).
2. **Add file > Upload files** y sube todos los archivos de esta carpeta (ya con `config.js` editado).
3. **Settings > Pages**: en *Source* elige **Deploy from a branch**, rama `main`, carpeta `/ (root)` y guarda.
4. En 1–2 minutos queda en `https://TU_USUARIO.github.io/barrenacion-larga/`.

## 3. Pasar los datos de la versión anterior (una sola vez)

1. Abre la página, escribe tu nombre y pulsa **Editor** (arriba a la derecha).
2. Escribe la clave de editor.
3. Pulsa **Importar datos de la versión anterior**. Al terminar verás los proyectos, el avance, la bitácora y el historial.

## Uso

- **Todos** (con el enlace): registrar barrenado (con equipo) y tumbado, ver tablero general, avance, bitácora, historial y descargar el reporte PDF.
- **Editores** (con la clave): además agregar proyectos nuevos, enviarlos al historial y restaurarlos.
- No hay opción de *Corregir a por barrenar* ni de editar o eliminar registros de la bitácora; las reglas de Firebase tampoco lo permiten.
- **Proyectos nuevos**: manda el PDF del plano a Claude; te devuelve un archivo `.json` que subes con **+ Nuevo proyecto**.

## Notas de seguridad

- Cualquier persona que tenga el enlace puede consultar y registrar avances. Compártelo solo con tu equipo.
- La clave de editor oculta las opciones de editor en la app, pero no es una protección fuerte. Las reglas de Firebase impiden borrar o modificar la bitácora y los proyectos cargados.
