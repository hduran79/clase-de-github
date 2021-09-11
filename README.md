# Manual Git

1. Descargar e instalar [Git](https://git-scm.com/download/win)

2. Descargar e instalar [NodeJs](https://nodejs.org/es/download/)

3. Repositorio [GitHub](https://github.com/)

```
user: hugoivandr@gmail.com
pass: hugo.duran79**
```

## Estrategias de Ramas

- https://jesuslc.com/2015/12/30/estrategias-de-branching-no-solo-existe-git-flow/
- https://www.atlassian.com/es/git/tutorials/comparing-workflows/gitflow-workflow#:~:text=El%20flujo%20de%20trabajo%20de,de%20la%20publicaci%C3%B3n%20del%20proyecto.

## Tutoriales

- https://www.youtube.com/watch?v=HiXLkL42tMU -> Basico
- https://www.youtube.com/watch?v=ZA23SFendmg -> Avanzado

## Configurar las variables globales de GIT

    git config --global --list -> Para verificar la configuracion global
    git config --global user.name "hduran"
    git config --global user.email hduran@votresas.com

# Que es GIT

- Sistema control de versiones
- Sistema que administra las distintas versiones de un archivo.
- Open Source, creado por Linux Torvalds
- Sistema de control distribuido -> Múltiples desarrolladores pueden alterar el código, los desarrolladores tienen una copia local, de esta manera estamos seguros que tenemos los últimos cambios del código
- Manejar cambios -> Se puede ir a versiones anteriores.
- Trabajar con repositorios locales y remotos.

# Crear un repositorio desde cero

```
echo "# try-git-remote" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/hduran79/try-git-remote.git
git push -u origin main
```

# Push a un repositorio existente

```
git remote add origin https://github.com/hduran79/try-git-remote.git
git branch -M main
git push -u origin main
```

# Áreas de trabajo

**_Working Directory:_** Es donde se trabaja con los archivos locales.

**_Staging Area:_** Donde agregan los archivos para subirlos al repository.

**_Repository:_** Repositorio de archivos.

# Command

## Verificar si git esta instalado o su versión

```
    git --version
    git status
```

## Clonar un repositorio

    git clone <ruta_del_repositorio>

## Enviar información del repositorio local al remoto

    git push origin <rama>

## Traer información del repositorio remoto a las rama locales

    git fetch origin <rama>
    ó
    git pull origin <rama>

## Zona Commit

    git revert HEAD (Elimina un commit completo y devuelve los cambios)

    git revert dc7f54d63a46d3310c3d681f17c0943fab9243bf
    git push -f origin master

    git reset --soft HEAD~1 (Elimina todo el commit y coloca los archivos en la zona del Staging Area)
    git reset --soft HEAD~1 <archivo> (Elimina un archivo del commit y lo coloca en la zona del Staging Area)

    git reset --mixed HEAD~1 (Elimina todo el commit y coloca los archivos en la zona Working directory)
    git reset --mixed HEAD~1 <archivo> (Elimina un archivo del commit y lo coloca en la zona Working directory)

    No recomendado
    git reset --hard HEAD~1 (Elimina todo el commit, quita los archivos de la zona de preparación y Staging Area, dejando los archivos origianles es decir borra los cambios)
    git reset --hard HEAD~1 <archivo> (Elimina un archivo del commit, y lo deja en a zona de preparación dejando el archivo original es decir borra los cambios)

## Ver las diferencias entre los archivos

    git diff (Muetra los cambios de los archivos en la zona del Working Directory o zona de preparación)
    git diff --staged (Muetra los cambios de los archivos en la zona del Staging Area)

# Cherry Pick (Copiar commit entre ramas)

    Ejemplo: Llevar un commit pero comitearlo
        1. Tengo dos ramas develop y feature/HU001
        2. En la rama feature/HU001 tengo el commit 7e7050f147c4bbd6d8cab662c31dd2728789233b y lo quiero llevar para develop
        3. Me ubico en develop y ejecuto el siguiente comando:
            git cherry-pick 7e7050f147c4bbd6d8cab662c31dd2728789233b
            o no comitiar el cherry pick
            git cherry-pick 7e7050f147c4bbd6d8cab662c31dd2728789233b --no-commit
        4. Hacer push para subir los cambios a develop

        Ejemplo 2: Llevar un commit pero sin comitearlos
        1. Tengo dos ramas develop y feature/HU001
        2. En la rama feature/HU001 tengo dos commits d7821aced0b6183fdc0e673ccd5023afd53d6eef y c0c79730607ac4a32e3b9037081e45c0dc7910e1 y lo quiero llevar para develop
        3. Me ubico en develop y ejecuto el siguiente comando:
            git cherry-pick -n c0c7973
            git cherry-pick -n d7821ac
        4. Hacer un git status para verificar que los commits estan el zona de staging area
        5. Hacer push para subir los cambios a develop

# Stash

Almacenar los cambios en una zona virtual y funciona como una pila.

    git stash -> Para guardar los cambios en la zona virtual.
    git stash list -> Listado de todos los elementos del stash
    git stash pop <stash{0}> -> para recuperar el commit y lo borra del stash
    git stash apply <stash{0}> -> para recuperar el commit pero no lo borra del stash

    Crear una rama a partir de un stash
    1. git stash
    2. git stash branch <nameBranch> -> Crea una rama con lo que hay en el stash

# Bisect

Es una forma eficiente de buscar en grupos grandes de datos (ordenados), es muy útil para buscar un trozo de código o un cambio no deseado en un commit. ver [tutorial](https://apiumhub.com/es/tech-blog-barcelona/git-bisect/#:~:text=Bisect%20es%20un%20algoritmo%20de,y%20adem%C3%A1s%20no%20es%20invasivo)

Luego necesitamos marcar dos commits como good (bueno) y bad (malo)

Ejemplo:

1. En primer lugar, inicializamos la búsqueda con:

```
git bisect start
```

2. Se marcan dos commits como good (bueno) y bad (malo) para especificar los límites de búsqueda. Marcaremos el HEAD actual como malo, ya que el bug se está reproduciendo en la actualidad:

```
git bisect bad
```

3. Ahora se marca el punto en el que estamos seguros que todo funcionaba correctamente. Se puede especificar mediante el SHA, tag o branch del commit, o simplemente haciendo checkout a un commit en concreto y marcarlo como bueno:

```
git checkout XXXXXXX
git bisect good
ó
git bisect good 1234567
```

4. Esto es Opcional dependiendo la cantidad de commit existentes, Git empezará a mover el HEAD entre commits ofreciéndonos la posibilidad de verificar el estado del código en cada momento. Las instrucciones son bastante explícitas, y nos podemos encontrar algo como:

```
Bisecting: 191 revisions left to test after this (roughly 8 steps)
[commit_123] Add new transaction endpoin
```

5. Al final ejecutar un reset para dejar todo original

```
git bisect reset
ó
rm .git/BISECT_*
```

# Blame

Muestra información de los cambios

```
git blame <archivo>
```

# Fusionar dos ramas MERGE

1. Me ubico en la rama a donde quiero que se actualice

```
git checkout develop
```

2. Ejecuto el siguiente comando, es decir voy a traer los cambios de la rama feature/HU001 para develop

```
git merge --no-ff feature/HU001
```

# Squash

Fusionar los mensajes de N commits en un solo mensaje

1. Listar todos los commits

```
git log --oneline
    612f2f7 This commit should not be squashed
    d84b05d This commit should be squashed
    ac60234 Yet another commit
    36d15de Rebase from here
    17692d1 Did some more stuff
    e647334 Another Commit
    2e30df6 Initial commit
```

2. Fusionar los commit desde el 612f2f7 hasta 36d15de

```
git rebase -i 36d15de
```

3. Automaticamente se abre el archivo rebase y se debe cambiar los pick por (tecla insert, al primer commit cambiar pick por REWORD y los demás por FIXUP):

```
    reword 612f2f7 El nuevo mensaje del commit
    fixup d84b05d This commit should be squashed
    fixup ac60234 Yet another commit
    fixup 36d15de Rebase from here
    :wq
    El nuevo mensaje del commit
    :wq
```

# Borrar ramas locales

```
git branch -a -> Lista las ramas locales y remotas
git branch -d <rama> -> Borrar una rama local
git push origin :nombre-rama -> Borrar una rama remota
```

# Recuperar una rama borrada

[Ejemplo](https://platzi.com/clases/1557-git-github/19988-git-reset-y-reflog-usese-en-caso-de-emergencia/)

```
git reflog (Recupera todos los movimientos del proyecto.)
git reset --hard <hash> (Recupera todo y borra todo justo antes del commit, borra la historia)
```

# Git Graph

```
gitk --all
git log --oneline --graph --color --all --decorate
```

# Quitar archivos de la Zona Staging Area

```
    git reset head .
    git reset head <archivo>
    git restore --stage .
    git restore --stage <archivo>
```

# Subir archivos a la Zona Staging Area

```
git add .
git add <archivo>
```

# Zona de preparación

## Borrar un archivo

```
rm <archivo>
```

## Descartar cambios

```
git checkout -- index.html
git restore <archivo>
```

# Borrar Tag

1. git tag --delete 1.0.0
2. git push --delete origin 1.0.0

# Manejo nombramiento de ramas

**feature/xxxxx** -> Rama que se crea para nuevas funcionalidades

**hotfix/my-bug-id** -> Rama que se crean para solucionar errores lo antes posible, no dan espera.

**bugfix/my-bug-id** -> Rama que se crean para corrección de errores

# .gitignore

Se debe crear un archivo .gitignore y agregar los archivos que no queremos que se suban al repositorio.

## Solucionar error name file long, execute with admin

git config --system core.longpaths true

# Plantillas para gitignore

https://github.com/github/gitignore

# Git Hooks

https://githooks.com/

# COMMIT

```
git add . -> agregar archivos al Staging Area
git commit -m "mensaje" -> Subir los cambios repositorio
```

## Remendar commits

```
git commit --amend -> Los cambios que hice los va a pegar al commit anterior, no hace un nuevo commit, pero si se puede cambiar el mensaje del mismo
```
