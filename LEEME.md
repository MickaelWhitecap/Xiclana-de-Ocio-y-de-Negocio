# Guía paso a paso: tu sitio de Chiclana que se actualiza solo

Tiempo estimado: unos 30 minutos, una sola vez. Coste: 0 €. No necesitas saber programar: solo hacer clic y copiar/pegar.

## 1. Qué es cada cosa (vocabulario)

- **GitHub**: una web gratuita (github.com) donde se guardan archivos. La usaremos como "almacén" y como "máquina que trabaja por ti".
- **Repositorio**: una carpeta tuya dentro de GitHub. Aquí guardaremos los archivos del sitio.
- **GitHub Actions**: un robot de GitHub. Le das unas instrucciones escritas en un archivo y las cumple solo, en el horario que le digas.
- **GitHub Pages**: el servicio de GitHub que convierte tu carpeta en una página web pública con su dirección.
- **OpenStreetMap (OSM)**: un mapa mundial gratuito que mantiene la gente, como una Wikipedia de mapas. Contiene comercios y lugares con nombre, dirección, teléfono, web y horario.
- **JSON**: un archivo de texto con datos ordenados. `data.json` es la lista de todos los sitios.

## 2. Cómo funciona (la idea completa)

Cada lunes de madrugada el robot de GitHub: (1) pregunta a OpenStreetMap "dame todos los comercios y lugares de Chiclana", (2) los ordena y los guarda en `data.json`, (3) añade tus fichas manuales de `manuales.json`, (4) publica la web con los datos nuevos. Tú no haces nada.

## 3. Qué hay en esta carpeta

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La página web que ven los visitantes. |
| `actualizar.py` | El programa que descarga y ordena los datos de OpenStreetMap. |
| `manuales.json` | Tus fichas escritas a mano (las 13 iniciales). Siempre tienen prioridad y nunca se borran. |
| `actualizar.yml` | Las instrucciones para el robot (cuándo y qué hacer). |
| `LEEME.md` | Esta guía. |

## 4. Puesta en marcha

**Paso 1 – Cuenta.** Entra en github.com, pulsa **Sign up** y crea una cuenta con tu correo. Confirma el correo que te envíen.

**Paso 2 – Repositorio.** Con la sesión iniciada, pulsa el botón **+** (arriba a la derecha) y elige **New repository**.
- *Repository name*: escribe `chiclana`.
- Marca **Public** (público; es necesario para que la web sea gratuita).
- Marca **Add a README file**.
- Pulsa **Create repository**.

**Paso 3 – Subir los archivos.** En tu repositorio pulsa **Add file → Upload files**. Arrastra estos 4 archivos: `index.html`, `actualizar.py`, `manuales.json`, `LEEME.md`. Abajo pulsa **Commit changes** (significa "guardar").

**Paso 4 – Crear el archivo del robot.** Este archivo va dentro de una carpeta oculta, por eso se crea a mano:
1. Pulsa **Add file → Create new file**.
2. En el cuadro del nombre escribe exactamente `.github/workflows/actualizar.yml` (al escribir cada `/` GitHub crea una carpeta).
3. Abre el archivo `actualizar.yml` de esta carpeta con el Bloc de notas, selecciona todo (Ctrl+A), copia (Ctrl+C) y pega (Ctrl+V) en el cuadro grande de GitHub.
4. Pulsa **Commit changes** y confirma.

**Paso 5 – Activar la web.** Ve a **Settings** (pestaña de arriba del repositorio) → **Pages** (menú de la izquierda). En *Build and deployment → Source* elige **GitHub Actions**.

**Paso 6 – Primera ejecución.** Ve a la pestaña **Actions**. Si te pide activarlas, acepta. Elige **Actualizar sitio** (izquierda) → **Run workflow** → **Run workflow**. Espera de 2 a 5 minutos y recarga. Verás una línea con un símbolo:
- 🟡 amarillo: trabajando.
- ✅ verde: terminado.
- ❌ rojo: ha fallado. Pulsa sobre ella, copia el texto del error y envíamelo.

**Paso 7 – Ver tu web.** Su dirección será `https://TU_USUARIO.github.io/chiclana/` (cambia TU_USUARIO por el nombre de tu cuenta). También aparece en Settings → Pages.

Desde aquí, se actualiza sola cada lunes. Si subes cualquier archivo nuevo, también se actualiza en ese momento.

## 5. Cómo añadir o corregir una ficha a mano

Abre `manuales.json` en GitHub, pulsa el lápiz ✏️ y añade una ficha copiando este formato (cuidado con las comas entre fichas):

```
{"n":"Nombre del sitio","t":"negocio","c":"Categoría","a":"Dirección","p":"956000000","w":"https://ejemplo.es","d":"Descripción breve"}
```
`t` solo puede ser `"ocio"` o `"negocio"`. Pulsa **Commit changes**; la web se actualiza en unos minutos. Si una ficha manual tiene el mismo nombre que una de OpenStreetMap, gana la tuya.

Truco: cualquier negocio puede darse de alta gratis en openstreetmap.org, y aparecerá aquí en la siguiente actualización.

## 6. Límites que debes conocer

- OpenStreetMap **no tiene todos los negocios**, sobre todo los pequeños. Si falta uno, añádelo como ficha manual.
- Los horarios y teléfonos son tan buenos como los que haya introducido la gente.
- GitHub **desactiva las tareas programadas si el repositorio pasa 60 días sin ninguna actividad**. Te avisarán por correo; se reactiva con un clic en la pestaña Actions.
- Si la descarga falla un lunes, el programa se detiene a propósito y la web conserva los datos anteriores (nunca se queda vacía).
