# Operación Destrabe · Ruta de la empresa en Colombia

Página interactiva con tres niveles:

1. **Operación Destrabe** (título general).
2. **Plan Nacional de Estandarización y Racionalización de Trámites**, liderado por el DAFP, con la **estrategia transversal de identificación de trámites** (MinJusticia y DNP) como escalón siguiente.
3. **Ruta de la empresa en Colombia** (componente productivo): seis etapas con sus trámites y entidades. Es el núcleo de la página.

Archivos:

- `generar_ruta.py` contiene **todos los textos y datos** y genera la página.
- `index.html` es la página lista para publicar (se genera con el script).

## Cómo editar

Abre `generar_ruta.py`. Las secciones están numeradas:

| Sección | Qué cambia |
|---|---|
| 1. Textos generales | Título general, subtítulo, encabezado de la ruta, introducción, pie de página y etiquetas |
| 1b. MARCO | Los escalones de arriba: etiqueta, título, texto y quién lidera |
| 2. Colores | Fondo, texto y bordes en modo claro y oscuro |
| 3. Niveles de gobierno | Nombres y colores (Nacional, Departamental, Municipal, Privado) |
| 4. Entidades | Nombre, sector y nivel de cada entidad |
| 5. Etapas | Título, cifra destacada, trámites y tarjetas de entidades de cada etapa |
| 6. Transversales | Entidades del bloque inferior |

Reglas útiles:

- Para agregar un escalón, copia un bloque de `MARCO`. Cada uno baja un nivel hacia la derecha. El último, con `"destacado": True` y `"ancla": "ruta"`, enlaza a la ruta.
- En `"lidera"` van claves de `ENTIDADES` (por ejemplo `"funcpub"`, `"minjusticia"`, `"dnp"`). Si no hay entidades, deja la lista vacía.
- Para agregar una entidad, créala en `ENTIDADES` y luego cítala por su clave.
- Para agregar una etapa, copia un bloque de `ETAPAS` y cambia el `id`. El orden de la lista es el orden de la ruta.
- Si una clave no existe, el script se detiene y dice cuál es.
- Los textos aceptan HTML simple: `<b>negrita</b>` o `<a href="https://...">enlace</a>`.
- `"no_verificado": True` agrega un asterisco (*) a lo que no pudo confirmarse en las fuentes.

## Generar `index.html`

**En Google Colab**
1. Entra a <https://colab.research.google.com> y crea un cuaderno nuevo.
2. Pega todo el contenido de `generar_ruta.py` en una celda y ejecútala.
3. Verás una vista previa y se descargará `index.html`.

**En tu computador**
```bash
python generar_ruta.py
```

## Publicar en GitHub Pages

1. Crea una cuenta en <https://github.com> si no la tienes.
2. Pulsa **+ → New repository**. Nombre: `ruta-tramites`. Márcalo **Public**. Pulsa **Create repository**.
3. Pulsa **uploading an existing file** (o **Add file → Upload files**), arrastra `index.html`, `generar_ruta.py` y `README.md`, y pulsa **Commit changes**.
4. Ve a **Settings → Pages**. En *Build and deployment* elige **Deploy from a branch**, rama **main** y carpeta **/ (root)**. Pulsa **Save**.
5. Espera uno o dos minutos. Tu página queda en `https://TU_USUARIO.github.io/ruta-tramites/`.

## Vincular el .html desde GitHub y desde otros sitios

La dirección de `index.html` dentro del repositorio (`github.com/.../blob/main/index.html`) muestra el **código**, no la página. Para que se vea la página usa siempre la dirección de GitHub Pages: `https://TU_USUARIO.github.io/ruta-tramites/`.

**Desde la portada del repositorio.** En la página principal del repositorio pulsa el engranaje junto a *About*, escribe la dirección de Pages en *Website* (o marca *Use your GitHub Pages website*) y guarda.

**Desde el README del repositorio.** Agrega una línea con el enlace en Markdown:
```markdown
[Ver la página](https://TU_USUARIO.github.io/ruta-tramites/)
```

**Desde tu perfil de GitHub.** Crea un repositorio público con el mismo nombre que tu usuario (`TU_USUARIO/TU_USUARIO`), agrega un `README.md` y pon el mismo enlace.

**Desde otra página HTML.**
```html
<a href="https://TU_USUARIO.github.io/ruta-tramites/" target="_blank" rel="noopener">Operación Destrabe</a>
```

**Incrustada en otra página** (si ese sitio permite iframes):
```html
<iframe src="https://TU_USUARIO.github.io/ruta-tramites/"
        style="width:100%;height:1400px;border:0" title="Operación Destrabe"></iframe>
```

**Entre varios .html del mismo repositorio.** Sube los archivos a la misma carpeta y enlázalos con rutas relativas, por ejemplo `<a href="otra-pagina.html">Otra página</a>`. Quedan en `https://TU_USUARIO.github.io/ruta-tramites/otra-pagina.html`.

**Abrir un bloque concreto.** La página abre una etapa si agregas su `id` al final del enlace, por ejemplo `.../ruta-tramites/#tributaria` (los ids son `registro`, `laboral`, `tributaria`, `operacion`, `control`, `cierre`).

## Actualizar

1. Cambia los textos en `generar_ruta.py` y ejecútalo de nuevo (Colab o local).
2. En GitHub abre el repositorio, pulsa **Add file → Upload files**, sube el nuevo `index.html` (reemplaza al anterior) y haz **Commit**.
3. En uno o dos minutos la página publicada se actualiza.

Para un cambio pequeño de texto puedes abrir `index.html` en GitHub, pulsar el lápiz (Edit) y modificar el bloque `var DATOS = {...}`. Si más tarde vuelves a ejecutar el script, ese cambio se sobrescribe, así que repítelo en `generar_ruta.py`.

## Con la línea de comandos (opcional)

```bash
git init
git add index.html generar_ruta.py README.md
git commit -m "Operación Destrabe: marco y ruta de la empresa"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/ruta-tramites.git
git push -u origin main
```

## Fuentes

CONPES 3956 de 2019 (DNP), Doing Business en Colombia 2017 (Banco Mundial), Decreto-Ley 2106 de 2019, Ley 2052 de 2020 y CONPES 4208 de 2026. El asterisco (*) marca información que las fuentes revisadas no confirman.
