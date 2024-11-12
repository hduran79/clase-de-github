# Que es GIT
Git es un software de control de versiones distribuido. El control de versiones es una forma de guardar cambios a lo largo del tiempo sin sobrescribir versiones anteriores. Estar distribuido significa que cada desarrollador que trabaja con un repositorio de Git tiene una copia de ese repositorio completo: cada confirmación, cada rama, cada archivo. 

* Git almacena los cambios en los hash (SHA), que funcionan comprimiendo archivos de texto. Eso hace que Git sea un muy buen sistema de control de versiones (VCS) para la programación de software, pero no tan bueno para archivos binarios como imágenes o videos.
* Los repositorios de Git se pueden conectar, por lo que puede trabajar en uno localmente en su propia máquina y conectarlo a un repositorio compartido. De esta manera, puede enviar y tirar cambios a un repositorio y colaborar fácilmente con otros.

# Herramientas
- GitKraken para manejar git desde una interfaz gráfica [Descargar](https://www.gitkraken.com/)
- Cmder para hacerlo mediante consola. [Descargar](https://cmder.net/)

# Explicación para simples mortales?
Git en pocas palabras es un comparador de textos. Detecta cada linea de nuestro código para buscar diferencias con respecto a lo que ya tenemos publicado en nuestro repositorio. Es importante entender que estamos “rascando la superficie” dado que Git es muy potente y tiene muchas funcionalidades. Pero en el sentido más práctico, es eso. [Clic Aquí](https://maxiburgos.medium.com/qu%C3%A9-es-git-y-c%C3%B3mo-instalarlo-b6102f4dec8)
# Git me sirve como back-up?
Si y no. Nos permite almacenar nuestro proyecto en la nube a través de GitHub o Bitbucket entre otros, o mantenerlo local en nuestra PC. Pero la utilidad mas importante es el trabajo colaborativo entre desarrolladores. Al tener un repositorio, vamos a poder subir los cambios y mantener un control de versionado. Pero a la vez otros desarrolladores pueden bajar esos cambios y mantener el proyecto actualizado. Entonces cuando nuestro compañero implementa una funcionalidad nueva y actualice el repositorio, nosotros vamos a poder bajar dichos cambios y trabajar con la última versión.

# Git, es pago?
Git es Open Source (Código Abierto) y gratuito. No hace falta pagar una licencia ni nada por el estilo. Se puede descargar desde su página oficial [Descargar](https://git-scm.com/).

# Puedo usar Git con cualquier lenguaje de programación o framework?
Efectivamente, pero es importante tener en cuenta que cada proyecto dependiendo de su tecnología va a tener una configuración determinada. Esto implica que existen ciertos archivos locales que se deben ignorar y no ser commiteados, como en el caso de la carpeta node_modules en proyectos de NodeJS. 
# Manual Git 👻

1. Descargar e instalar [Git](https://git-scm.com/download/win)

2. Descargar e instalar [NodeJs](https://nodejs.org/es/download/)

3. Repositorio [GitHub](https://github.com/)

```
user: hugoivandr@gmail.com
pass: XXXXX
```

## Estrategias de Ramas

- https://jesuslc.com/2015/12/30/estrategias-de-branching-no-solo-existe-git-flow/
- https://www.atlassian.com/es/git/tutorials/comparing-workflows/gitflow-workflow#:~:text=El%20flujo%20de%20trabajo%20de,de%20la%20publicaci%C3%B3n%20del%20proyecto.

## Tutoriales

- https://www.youtube.com/watch?v=HiXLkL42tMU -> Básico
- https://www.youtube.com/watch?v=ZA23SFendmg -> Avanzado

## Configurar las variables globales de GIT

    git config --global --list -> Para verificar la configuración global
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

``` sh
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
[documentación](https://juncotic.com/git-reset-y-git-reverse/)
**RESET**
Git reset se utiliza para mover el proyecto a un commit anterior eliminando todos los posteriores de el historial de commits.
### Puede utilizarse reset cuando:

* Se han hecho commits equivocados no publicados y se desea deshacer los cambios: En el caso de no querer mantener ningunos de los cambios locales realizados puede utilizarse –hard, en caso contrario, si se quieren mantener esos cambios para realizar un commit con ellos más adelante puede utilizarse –soft.
* Se han publicado commits cuya información se desea eliminar del historial permanentemente..

### DESHACER EL ÚLTIMO COMMIT - NO debe utilizarse reset cuando:

* Se quiere regresar el proyecto al estado de un estado anterior pero se quiere mantener registros de esos cambios. En este caso debe utilizarse reverse.
* Se está trabajando en proyecto entre más de una persona y no existen un consenso grupal sobre el revertido permanente.
* Video https://www.youtube.com/watch?v=HZ1c25OIX4o

``` sh
git reset HEAD~1 (Elimina todo el commit y coloca los archivos en la zona Working directory)

git reset --soft <commit> (Elimina todo el commit y coloca los archivos en la zona del Staging Area)
git reset --soft <commit> <archivo> (Elimina un archivo del commit y lo coloca en la zona del Staging Area)

git reset --mixed <commit> (Elimina todo el commit y coloca los archivos en la zona Working directory)
git reset --mixed <commit> <archivo> (Elimina un archivo del commit y lo coloca en la zona Working directory)

No recomendado
Elimina todo el commit, quita los archivos de la zona de preparación y Staging Area, dejando los archivos originales es decir borra los cambios
git reset --hard <commit> 
git reset --hard <commit> <archivo> 
```

**REVERT**
Git reverse revierte el proyecto al estado de un commit generando un nuevo commit que revierte los cambios realizados. De esta manera las modificaciones no son eliminadas del historial y pueden ser accedidas en el futuro. Los cambios locales que no han sido guardados son sobrescritos.
``` sh
git revert HEAD (Elimina un commit completo y devuelve los cambios)
git revert 3291691874ccea8fb06508fe8c2f58bdb9c272a4
git push -f origin master
```

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

    1. Agregar los cambios en el Staging Area y después ejecutar los comandos del stash
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
git push origin --delete :nombre-rama -> Borrar una rama remota
```

# Renombrar rama local

```
git branch -m old_branch new_branch
```


# Reestablecer al commit requerido

Es importante cuando queremos dejar una rama en su estado original

[Ejemplo](https://platzi.com/clases/1557-git-github/19988-git-reset-y-reflog-usese-en-caso-de-emergencia/)

```
git reflog (Recupera todos los movimientos del proyecto.)
git reset --hard <hash> (Recupera todo y borra todo justo antes del commit, borra la historia)
```

# Recuperar una rama borrada

```
git reflog (Recupera todos los movimientos del proyecto.)
git checkout -b <nameBranch> <hash>
```

# Git Graph

```
gitk --all
git log --oneline --graph --color --all --decorate
tig
```

# Quitar archivos de la Zona Staging Area

``` sh
    git reset head .
    git reset head <archivo>
    git restore --staged .
    git restore --staged <archivo>
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
git checkout -- index.html (quita el archivo de steagen area y lo pasa al working directory)
git restore <archivo> (Elimina los cambios del archivo que esta en el working directory)
```

# Tag

1. Listar Tags
git tag -l

2. Borrar
git tag --delete 1.0.0

3. Borrar tag Remoto
git push --delete origin 1.0.0

4. Crear branch a partir de un Tag
    git checkout -b nameBranch versionTag

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

## MODIFICAR EL MENSAJE DEL ÚLTIMO COMMIT
Suponemos que acabamos de hacer un commit en el repositorio pero nos hemos olvidado de añadir un archivo que queremos incluir en ese commit. En estos casos podemos utilizar el comando git commit --amend para añadir nuevos archivos al último commit realizado sobre el repositorio.

A continuación se muestra una posible secuencia de comandos simulando la situación que acabamos de describir.

Pero justo después de hacer el commit nos damos cuenta de que el mensaje no es totalmente correcto y queremos modificarlo. Para corregirlo, usaremos la opción --amend, de la siguiente manera:

``` sh
git add archivo.txt
git commit -m "Añadimos el archivo.txt"
git add archivo_olvidado.txt
git commit -m "nuevo mensaje del commit" --amend
```

# Deshacer cambios en el workspace
Para deshacer los cambios realizados en archivo.txt y volver a su estado anterior sería necesario ejecutar:

``` sh
git ckeckout -- archivo.txt
```
# Borrando y moviendo/renombrando archivos

1. Queremos eliminar un archivo que todavía no ha sido incluido en el repositorio y se encuentra en la sección Workspace con el estado Untracked. 
   En este caso no es necesario utilizar ningún comando específico de git, lo borraríamos con el comando rm.
``` sh
rm archivo.txt
```

2. Queremos eliminar un archivo que ya está incluido en el repositorio y se encuentra en la sección Workspace con el estado Modified.
3. Queremos eliminar un archivo que ya está incluido en el repositorio y se encuentra en la sección Staging Area con el estado Staged.
4. Queremos eliminar un archivo que ya está incluido en el repositorio y se encuentra en la sección Local Repository con el estado Commited.
``` sh
git rm archivo.txt
git commit -m "Se elimina archivo.txt"
```

# Mover/Renombrar archivos
Para mover a otro directorio o renombrar un archivo que ya se encuentra bajo el control de versiones de git es necesario utilizar el siguiente comando:
``` sh
git mv archivo.txt nuevo_nombre.txt
git commit -m "Se renombra archivo.txt por nuevo_nombre.txt"
```
# Utilidades

[Pages Github](https://pages.github.com/)
[Editor MarkDown](https://pandao.github.io/editor.md/en.html)

# Desbloquear un archivo Git
``` sh
git lfs locks => list all locked files
git lfs unlock JenkinsfileWeb => unlock file, fail if the file was locked
git lfs unlock --id=17 --force => force to unlock the file
```

# Git Remote 

Verificar el repositorio al cual esta link el proyecto
``` sh
$ git remote -v

origin  https://github.com/platzi/nestjs-modular.git (fetch)
origin  https://github.com/platzi/nestjs-modular.git (push)

link al proyecto nuevo
git remote set-url origin https://gitlab-dso.serviciosit.co/votre/self-registration/votre.selfregistration.selfregistrationcountryassembly.git
```

link al proyecto nuevo
``` sh
git remote set-url origin https://gitlab-dso.serviciosit.co/votre/self-registration/votre.selfregistration.selfregistrationcountryassembly.git

o 

git remote set-url origin $(git remote -v | awk 'NR==1{print $2}' | awk '{gsub("git-dso.leonisa.com", "gitlab-dso.serviciosit.co");}1')
```

Remover el repositorio al cual esta link el proyecto.
``` sh
$ git remote rm origin

git remote add origin https://github.com/platzi/nestjs-typeorm-datos.git
git remote rm origin

git remote add origin https://github.com/hduran79/nestjs-typeorm-datos.git
git remote rm origin
```

git info remote
``` sh
 git remote show origin
<<<<<<< HEAD
```

# hashes más cortos
git log --oneline
=======
```
>>>>>>> parent of 0542d5d (Hashes mas cortos)
