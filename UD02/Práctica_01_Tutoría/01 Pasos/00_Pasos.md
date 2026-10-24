# Práctica 01 — Primeros pasos con Git

## Parte 1: Configuración y creación del repositorio

### 1. Configurar Git

La configuración global (`--global`) se guarda en `~/.gitconfig` y se aplica a todos los repositorios del equipo.

1. **Identidad**: indicamos quiénes somos para que cada commit quede firmado con su autor.
   ```bash
   git config --global user.name "Nombre Apellido"
   git config --global user.email "correo@ejemplo.net"
   ```
2. **Colores**: para ver la salida de Git en colores en la consola.
   ```bash
   git config --global color.ui auto
   ```
3. **Rama principal**: hacemos que la rama inicial de los repositorios nuevos se llame `main`.
   ```bash
   git config --global init.defaultBranch main
   ```
4. **Comprobar la configuración** con `--list`:
   ```bash
   git config --list
   ```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#ce9178">user.name=Nombre Apellido</span>
<span style="color:#ce9178">user.email=correo@ejemplo.net</span>
<span style="color:#ce9178">color.ui=auto</span>
<span style="color:#ce9178">init.defaultbranch=main</span></pre>
</div>

### 2. Crear la carpeta del proyecto

Creamos la carpeta `repos/tienda` para el proyecto de la tienda online.

```bash
cd Documentos
mkdir -p repos/tienda
cd repos/tienda
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#4ec9b0">user@MintBase</span>:<span style="color:#569cd6">~/Documentos/repos/tienda</span>
Directorio de trabajo preparado.</pre>
</div>

### 3. Inicializar el repositorio

`git init` convierte la carpeta en un repositorio (crea la carpeta oculta `.git`). Con `git status` vemos el estado: estamos en la rama `main` y todavía no hay commits.

```bash
git init
ls -a
git status
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">Repositorio Git vacío inicializado.
<span style="color:#569cd6">.  ..  .git</span>
En la rama <span style="color:#6a9955">main</span>
Todavía no hay commits.</pre>
</div>

### 4. Crear `index.html`

Creamos la página principal de la tienda con `nano index.html`.

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#6a9955">&lt;!DOCTYPE html&gt;</span>
&lt;html lang="es"&gt;
   &lt;head&gt;
      &lt;meta charset="utf-8"&gt;
      &lt;title&gt;Tienda Online&lt;/title&gt;
   &lt;/head&gt;
   &lt;body&gt;
      &lt;h1&gt;Tienda Online&lt;/h1&gt;
   &lt;/body&gt;
&lt;/html&gt;</pre>
</div>

### 5. Añadir el archivo al área de preparación (staging)

`git status` muestra `index.html` en rojo como **archivo sin seguimiento**: Git lo ve, pero no lo controla todavía.

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">En la rama main
Archivos sin seguimiento:
   <span style="color:#ce9178">index.html</span></pre>
</div>

Con `git add` lo pasamos al área de preparación (*staging*) y ya aparece en verde como "cambios a ser confirmados".

```bash
git add index.html
git status
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">Cambios preparados para el commit:
   <span style="color:#6a9955">nuevo archivo: index.html</span></pre>
</div>

### 6. Primer commit

El commit guarda los cambios en el repositorio **local**, con un mensaje que describe lo que se ha hecho. (Para enviarlo a un servidor remoto se usaría `git push`.)

```bash
git commit -m "Añadimos el landing page de nuestra tienda"
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">[main <span style="color:#dcdcaa">31c3078</span>] Añadimos el landing page de nuestra tienda
 1 file changed, 13 insertions(+)
 create mode 100644 index.html</pre>
</div>

### 7. Ver el historial

`git log` muestra los commits: su identificador (hash), autor, fecha y mensaje. `HEAD -> main` indica el commit en el que estamos.

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">Author: Nombre Apellido &lt;correo@ejemplo.net&gt;
Date: 2026-10-13
<span style="color:#4ec9b0">HEAD -&gt; main</span> apunta al commit actual.</pre>
</div>

### 8. Modificar un archivo y ver las diferencias

Cambiamos el título de la página a "Tienda Online de Deportes".

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#6a9955">&lt;h1&gt;</span>Tienda Online de Deportes<span style="color:#6a9955">&lt;/h1&gt;</span></pre>
</div>

`git diff` muestra las diferencias entre el archivo modificado y la última versión guardada. Gracias a `color.ui auto`, las líneas eliminadas salen en rojo (`-`) y las añadidas en verde (`+`).

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#f48771">-    &lt;title&gt;Tienda Online&lt;/title&gt;</span>
<span style="color:#89d185">+    &lt;title&gt;Tienda Online de Deportes&lt;/title&gt;</span>
<span style="color:#f48771">-    &lt;h1&gt;Tienda Online&lt;/h1&gt;</span>
<span style="color:#89d185">+    &lt;h1&gt;Tienda Online de Deportes&lt;/h1&gt;</span></pre>
</div>

Tras volver a hacer `git add`, `git diff` queda vacío, porque el cambio ya está en staging. Para ver lo que está preparado y pendiente de confirmar se usa `git diff --staged`.

```bash
git add index.html
git diff            # vacío
git diff --staged   # muestra el cambio preparado
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#569cd6">git diff</span>: sin salida (cambios ya preparados)
<span style="color:#569cd6">git diff --staged</span>: 1 archivo modificado; el cambio de título está preparado.</pre>
</div>

Confirmamos el cambio:

```bash
git commit -m "Cambiamos el título de la página"
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">[main <span style="color:#dcdcaa">1966088</span>] Cambiamos el título de la página
 1 file changed, 2 insertions(+), 2 deletions(-)</pre>
</div>

### 9. Ver un commit con `git show`

`git show` muestra el último commit con sus cambios. Diferencia con `diff`:
- `git show` mira **hacia atrás**: lo que ya está en el historial.
- `git diff` mira **hacia delante**: lo que todavía no se ha confirmado.

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"> index.html | 4 <span style="color:#89d185">++</span><span style="color:#f48771">--</span>
 1 file changed, 2 insertions(+), 2 deletions(-)</pre>
</div>

### 10. Añadir una hoja de estilos

Creamos `style.css` y la enlazamos desde `index.html` con `<link rel="stylesheet" href="style.css">`.

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">style.css
<span style="color:#6a9955">h1</span> {
   background-color: steelblue;
   font-family: Arial, sans-serif;
   color: white;
}</pre>
</div>

Añadimos los dos archivos y hacemos commit:

```bash
git add index.html style.css
git commit -m "Añadida hoja de estilos"
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">[main <span style="color:#dcdcaa">c7f1708</span>] Añadida hoja de estilos
 2 files changed, 5 insertions(+)</pre>
</div>

Con `git show` vemos los cambios de ese commit en ambos archivos.

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"> index.html | 1 <span style="color:#89d185">+</span>
 style.css  | 5 <span style="color:#89d185">+++++</span>
 2 files changed, 6 insertions(+)</pre>
</div>

### 11. Ver quién cambió cada línea con `git blame`

`git blame` muestra, para cada línea de un archivo, el commit, el autor y la fecha del último cambio.

```bash
git blame index.html
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#dcdcaa">c7f1708</span> (Nombre Apellido 2026-10-13) 5) &lt;link rel="stylesheet" href="style.css"&gt;
<span style="color:#dcdcaa">1966088</span> (Nombre Apellido 2026-10-13) 6) &lt;title&gt;Tienda Online de Deportes&lt;/title&gt;
<span style="color:#dcdcaa">31c3078</span> (Nombre Apellido 2026-10-13) 9) &lt;h1&gt;Tienda Online&lt;/h1&gt;</pre>
</div>

### 12. Ignorar archivos con `.gitignore`

En el repositorio se guarda el código fuente, pero no cosas como configuraciones del equipo o secretos (contraseñas, claves...). En el archivo `.gitignore` se indica qué archivos y carpetas del proyecto **no** se guardan en el repositorio.

Para probarlo, creamos la carpeta `node_modules` con un archivo que simula contener una contraseña:

```bash
mkdir -p node_modules
touch node_modules/paquete.js
nano node_modules/paquete.js
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">node_modules/paquete.js
<span style="color:#ce9178">API_KEY="valor-ficticio-no-utilizable"</span></pre>
</div>

Creamos `.gitignore` con `nano .gitignore`. Se suele organizar por bloques:
- **Dependencias**: `node_modules/`, `vendor/`.
- **Configuración y secretos**: variables de entorno (`.env`) y archivos locales (`*.local`).
- **Artefactos de construcción**: carpetas generadas al compilar (`build/`, `dist/`).
- **Sistema operativo y editor**: `.DS_Store`, `.vscode/`.

Los directorios se escriben con barra al final. Existen plantillas de `.gitignore` para casos comunes (lenguajes, IDEs...).

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#6a9955"># Dependencias</span>
node_modules/
vendor/

<span style="color:#6a9955"># Configuración y secretos</span>
.env
*.local

<span style="color:#6a9955"># Artefactos de construcción</span>
build/
dist/

<span style="color:#6a9955"># Sistema operativo y editor</span>
.DS_Store
.vscode/</pre>
</div>

Al hacer `git status` solo aparece `.gitignore`: la carpeta `node_modules` ya no se muestra porque está ignorada.

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">Archivos sin seguimiento:
   <span style="color:#ce9178">.gitignore</span>
<span style="color:#6a9955">node_modules/ está ignorado</span></pre>
</div>

```bash
git add .gitignore
git commit -m "Añadido .gitignore del proyecto"
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">[main <span style="color:#dcdcaa">1dcff6f</span>] Añadido .gitignore del proyecto
 1 file changed, 16 insertions(+)
 create mode 100644 .gitignore</pre>
</div>

---

Hasta aquí la configuración del repositorio. Ahora veremos funcionalidades para **corregir errores**.

## Parte 2: Deshacer cambios

### 1. Descartar cambios sin confirmar con `git restore`

Añadimos una línea errónea al final de `index.html`:

```bash
echo "linea de codigo errónea" >> index.html
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">Línea añadida al final de index.html:
<span style="color:#ce9178">linea de codigo errónea</span></pre>
</div>

`git status` muestra el archivo como modificado y sugiere `git restore` para descartar los cambios.

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">Cambios no preparados:
   <span style="color:#ce9178">modificado: index.html</span>
<span style="color:#6a9955">git restore puede descartar estos cambios</span></pre>
</div>

`git restore` devuelve el archivo a su estado del último commit (si el cambio estuviera en staging, con `git restore --staged` lo sacaríamos del área de preparación).

```bash
git restore index.html
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">index.html restaurado al contenido del último commit.
<span style="color:#6a9955">La línea errónea ya no está presente.</span></pre>
</div>

### 2. Corregir el mensaje del último commit con `--amend`

Añadimos un comentario con el autor y hacemos commit. Con `-a` se añaden automáticamente todos los archivos ya seguidos que estén modificados, sin necesidad de `git add`.

```bash
echo '<!-- autor: nombre -->' >> index.html
git commit -a -m "Añade el autor y su correo"
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">[main <span style="color:#dcdcaa">da4e8d9</span>] Añade el autor y su correo
 1 file changed, 1 insertion(+)</pre>
</div>

El mensaje no es correcto (no se ha añadido ningún correo), así que lo editamos con `--amend`, que reemplaza el último commit por uno nuevo (cambia su hash):

```bash
git commit --amend -m "Añade el autor"
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">[main <span style="color:#dcdcaa">c26e040</span>] Añade el autor
 1 file changed, 1 insertion(+)
<span style="color:#6a9955">El commit anterior fue reemplazado por uno con un hash nuevo.</span></pre>
</div>

### 3. Volver atrás con `git reset`

`git log --oneline` muestra el historial resumido. `HEAD` es el commit donde estamos y con `HEAD~n` nos referimos a `n` commits atrás (con `~`, no con `-`: `HEAD-1` da error).

```bash
git log --oneline
git reset --soft HEAD~1
git reset --soft HEAD~2
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#f48771">fatal: argumento ambiguo 'HEAD-1'</span>
Usa <span style="color:#6a9955">HEAD~1</span> para referirte al commit anterior.
Después de <span style="color:#569cd6">git reset --soft HEAD~1</span>, los cambios permanecen en staging.</pre>
</div>

- `--soft`: deshace el commit pero conserva los cambios en staging.
- `--hard`: deshace el commit y **borra** el trabajo.

> `git reset` reescribe el historial, así que solo debe usarse con commits que aún no han salido de nuestra máquina. Si el error ya está publicado, se usa `git revert`, que crea un commit nuevo que deshace los cambios sin reescribir el historial.

---

## Parte 3: Alias e introducción a las ramas

Con `ls -a` podemos ver también los archivos y directorios ocultos. En la raíz del proyecto aparece `.git`, donde Git guarda los datos del repositorio; no debemos modificar su contenido manualmente.

> Si se elimina `.git`, no se borran los archivos del proyecto que están en la carpeta: queda la versión que hubiera en la rama activa, junto con los demás archivos presentes. Sin embargo, Git pierde el historial de commits, las ramas, la configuración del repositorio y los cambios preparados en *staging*. La carpeta deja de reconocerse como repositorio y `git status` ya no funciona allí. Ejecutar `git init` crearía un repositorio nuevo, sin recuperar el historial anterior.

### 1. Consultar el historial en forma de grafo

La opción `--graph` representa las ramas y los commits como un grafo. Combinada con `--oneline`, `--decorate`, `--color` y `--all`, permite consultar de forma compacta el historial de todas las ramas:

```bash
git log --oneline --all --graph --decorate --color
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#4ec9b0">* (HEAD -&gt; main)</span>
<span style="color:#4ec9b0">* ...</span>
<span style="color:#6a9955">Se omiten los commits ya descritos para evitar repetir sus mensajes.</span></pre>
</div>

### 2. Crear un alias para el historial

Un alias permite crear un nombre corto para un comando que usamos con frecuencia. Este alias global se llamará `hist` y ejecutará el comando anterior:

```bash
git config --global alias.hist "log --oneline --graph --decorate --color --all"
git hist
```

Los alias de Git se ejecutan como subcomandos: se escribe `git` seguido del nombre del alias.

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#4ec9b0">* main</span>
<span style="color:#4ec9b0">* feature/carrito</span> <span style="color:#6a9955">rama activa</span></pre>
</div>

### 3. Crear una rama para una funcionalidad

Una rama es una referencia a un commit que permite desarrollar cambios de forma independiente. Así podemos probar una funcionalidad sin incorporarla todavía a `main`. Creamos la rama `feature/carrito` y cambiamos a ella con `switch -c`:

```bash
git switch -c feature/carrito
git branch
```

`git branch` muestra las ramas locales; el asterisco identifica la rama activa. A continuación, creamos `carrito.js` con el editor:

```bash
nano carrito.js
```

### 4. Guardar la funcionalidad en la rama

Añadimos el archivo al área de preparación y confirmamos el cambio:

```bash
git add carrito.js
git commit -m "Añadimos el carrito a la compra"
git hist
```

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap">[feature/carrito] Añadimos el carrito a la compra
Commit creado en la rama de funcionalidad.</pre>
</div>

> `git add carrito.js` no quita del área de preparación otros cambios que ya estuvieran preparados. Como en el apartado anterior usamos `git reset --soft`, el commit puede incluir también esos cambios pendientes. Comprueba `git status` antes de confirmar si quieres que el commit contenga únicamente `carrito.js`.

### 5. Cambiar entre ramas

Al volver a `main`, `carrito.js` no aparece porque ese archivo solo se ha creado en `feature/carrito`. Al cambiar de nuevo a esa rama, vuelve a aparecer:

```bash
git switch main
ls
git switch feature/carrito
ls
```

Las ramas comparten el historial común, pero cada una puede mostrar una versión distinta de los archivos.

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#569cd6">En main:</span>
index.html  node_modules/  style.css

<span style="color:#569cd6">En feature/carrito:</span>
carrito.js  index.html  node_modules/  style.css</pre>
</div>

### 6. Crear una rama para corregir un error

Partimos de `main` y creamos `hotfix/titulo` para preparar una corrección sin modificar directamente la rama principal:

```bash
git switch main
git switch -c hotfix/titulo
git branch
```

En este ejemplo, cambiamos el título de `index.html`. `sed` distingue entre mayúsculas y minúsculas, por lo que el texto buscado debe coincidir con el título actual:

```bash
sed -i 's/Tienda Online de Deportes/Deportes Strong/' index.html
git diff
git commit -a -m "Cambiado el título a nombre corporativo"
```

El cambio queda confirmado en `hotfix/titulo`; `main` todavía conserva el título anterior hasta que fusionemos la rama.

## Parte 4: Integrar ramas y resolver conflictos

### 1. Fusionar cambios en `main`

Una vez revisados los cambios de una rama, podemos integrarlos en `main`. Primero cambiamos a la rama de destino y fusionamos `hotfix/titulo`:

```bash
git switch main
git merge hotfix/titulo
```

Como `main` no tenía cambios propios desde que se creó `hotfix/titulo`, Git puede avanzar `main` hasta el commit de la corrección (*fast-forward*). El título actualizado también se verá al abrir `index.html` desde la carpeta de trabajo.

Después integramos la funcionalidad del carrito:

```bash
git merge feature/carrito
```

En este caso, Git crea un commit de fusión porque las ramas tienen commits distintos. Si aparece el editor del mensaje, podemos conservar el mensaje propuesto y guardar y cerrar el editor para terminar la fusión.

### 2. Consultar y eliminar ramas integradas

`--merged` lista las ramas cuyos cambios ya están integrados en la rama actual; `--no-merged` muestra las que todavía no lo están. `-d` elimina una rama integrada y se niega a borrarla si detecta cambios sin fusionar.

```bash
git branch --merged
git branch --no-merged
git branch -d hotfix/titulo
git branch -d feature/carrito
git branch
```

`-D` fuerza el borrado incluso si la rama no está integrada; puede hacer inaccesibles sus commits, así que no debe usarse como opción habitual.

### 3. Provocar y reconocer un conflicto

Para practicar un conflicto, creamos `cambio-a` y modificamos el título en esa rama:

```bash
git switch -c cambio-a
sed -i 's/Deportes Strong/Deportes Fit/' index.html
git commit -a -m "Cambio a Deportes Fit"
```

Mientras tanto, hacemos otro cambio en `main` sobre esa misma línea:

```bash
git switch main
sed -i 's/Deportes Strong/Deportes Lolita/' index.html
git commit -a -m "Cambio a Deportes Lolita"
git merge cambio-a
```

Como ambas ramas modificaron la misma línea de forma distinta, Git no puede decidir qué versión conservar. La fusión se detiene y `git status` identifica `index.html` como archivo en conflicto:

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#4ec9b0">user@MintBase</span>:<span style="color:#569cd6">~/Documentos/repos/tienda</span>$ git merge cambio-a
Auto-fusionando index.html
CONFLICTO (contenido): Conflicto de fusión en index.html
La fusión automática falló; arregle los conflictos y luego realice un commit con el resultado.
<span style="color:#4ec9b0">user@MintBase</span>:<span style="color:#569cd6">~/Documentos/repos/tienda</span>$ git status --short
UU index.html</pre>
</div>

Abre `index.html` en un editor de texto, no en el navegador. Git inserta estos marcadores en el archivo para señalar las dos versiones en conflicto. `HEAD` identifica el contenido de la rama actual (`main`); después de `=======` aparece la versión de `cambio-a`. Los signos `-` y `+` no forman parte del archivo: son propios de una salida de `git diff`.

<div style="background:#1e1e1e;color:#d4d4d4;padding:0.8em 1em;border-radius:6px;overflow-x:auto">
<pre style="margin:0;white-space:pre-wrap"><span style="color:#ce9178">&lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD</span>
   &lt;h1&gt;Deportes Lolita&lt;/h1&gt;
<span style="color:#d4d4d4">=======</span>
   &lt;h1&gt;Deportes Fit&lt;/h1&gt;
<span style="color:#6a9955">&gt;&gt;&gt;&gt;&gt;&gt;&gt; cambio-a</span></pre>
</div>

Editamos el archivo, elegimos el contenido final y quitamos todos los marcadores. En este ejemplo conservamos `Deportes Lolita`. Después marcamos el conflicto como resuelto y completamos el commit de fusión:

```bash
git add index.html
git commit
git hist
```

Si no queremos continuar con la fusión, podemos cancelarla con `git merge --abort` antes de resolver y confirmar los cambios.

## Parte 5: Conectar el repositorio con GitHub por SSH

Hasta ahora el repositorio es local: si el equipo falla, podríamos perder el trabajo. Un repositorio remoto en GitHub o GitLab permite alojar una copia y compartirla.

### 1. Crear una clave SSH

Generamos un par de claves Ed25519. El comentario ayuda a identificar la clave; se recomienda proteger la clave privada con una frase de contraseña. No compartas el archivo privado `~/.ssh/id_ed25519`.

```bash
ssh-keygen -t ed25519 -C "usuario@equipo"
```

- `ssh-keygen` crea y administra pares de claves para autenticarse mediante SSH.
- `-t ed25519` selecciona Ed25519, un algoritmo moderno de firma digital basado en curvas elípticas. Se usa para demostrar que controlamos la clave privada sin enviarla al servidor.
- `-C "usuario@equipo"` añade un comentario identificativo a la clave; no es una contraseña ni cambia cómo funciona la clave.

El comando pregunta dónde guardar el par y si queremos proteger la clave privada con una frase de contraseña. Aceptar la ruta predeterminada crea `~/.ssh/id_ed25519` (privada) y `~/.ssh/id_ed25519.pub` (pública). La clave pública se comparte con GitHub; la privada permanece en el equipo.

La clave pública, que sí podemos añadir a GitHub, termina en `.pub`:

```bash
cat ~/.ssh/id_ed25519.pub
```

En GitHub, vamos a **Settings > SSH and GPG keys > New SSH key**, ponemos un nombre para identificar el equipo y pegamos el contenido de la clave pública. Nunca pegamos ni compartimos la clave privada.

### 2. Añadir el remoto y subir `main`

Creamos primero un repositorio vacío en GitHub y copiamos su dirección SSH. Sustituimos `USUARIO` por el nombre de la cuenta:

```bash
git remote add origin git@github.com:USUARIO/tienda_DAWB.git
git remote -v
git push -u origin main
```

`origin` es el nombre convencional del remoto y `-u` deja configurada la rama remota de seguimiento para futuros `git push` y `git pull`.

Si el `push` termina con «Could not read from remote repository», no se ha subido el repositorio. Comprueba que el repositorio existe, que la URL corresponde a tu cuenta y que la clave pública está añadida a GitHub con permisos de acceso. También puedes probar la conexión con:

```bash
ssh -T git@github.com
```

Al conectar por primera vez, verifica la identidad del servidor antes de aceptar su clave.
