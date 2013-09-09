Para hacer checkin inicial del wordpress a git, sabiendo que `jeo` ya
es un repositorio git cloneado, primero chequineamos nuestros cambios
a `jeo`:

      cd wp-content/themes/jeo
      git add languages/

      git reset HEAD languages/es_ES.po~
      git commit -m 'added missing strings to Spanish translation'

      git add css/main.css css/main.less
      git commit -m 'tweak to map look and feel for Sementes Desobedientes to work better on small screens'

Cloneé el repo en github; ahora pusheamos nuestros cambios a nuestro
propio repo, así que podremos después clonearlo para hacer nuestro
submodulo:

      git remote add github https://github.com/aelevadoan/jeo.git
      git push -u github master

Ahora reemplazamos el repo que habíamos cloneado de lo de cardume, con
uno que cloneamos de nuestro propio repo de github, porque no sé cómo
se agrega un checkout que ya existe como un submodulo:

      cd ../../..
      cd wp-content/themes
      mv jeo jeo.orig
      git submodule add https://github.com/aelevadoan/jeo.git jeo

Y bueno, ahora agregamos el resto de los archivos:

      cd ../..
      git add .

Pero no queremos el directorio uploads en el chequin:

      cd wp-content
      git rm --cached uploads -r

Listo:

      git commit -m 'initial checkin of wordpress with JEO'

Ahora pusheamos a nuestro repo:

      git remote add origin https://github.com/aelevadoan/wordpress-con-jeo.git
      git push -u origin master

      cd ../..

Y ahora testeamos clonearlo:

      mv wordpress/ wordpress.orig
      git clone https://github.com/aelevadoan/wordpress-con-jeo.git wordpress
      cd wordpress
      git submodule init
      git submodule update

Con estos cuatro últimos comandos, podés clonear nuestra instalación
de wordpress en tu propio servidor.  Tendrá los credenciales para
nuestra instalación de MySQL.  Probablemente tendrás que reconfigurar
o MySQL o WordPress (en `wordpress/wp-config.php`) para hacerlo andar.
Tenemos también un archivo `wordpress-contents.tar.gz` con un SQL dump
y los imágenes subidas.