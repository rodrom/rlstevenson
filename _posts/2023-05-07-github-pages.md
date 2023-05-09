---
title: "Configurar Github Pages de un repositorio como este"
author: rodrom
---

Para poder desarrollar y testear en un entorno local tu cuaderno de bitácoras virtual
usando la aplicación de microblogging [Jekyll](https://jekyllrb.com/) mediante la configuración
por defecto que ofrece [Github](https://github.com) para un repositorio que reside como subdirectorio en
la dirección por defecto de [Github Pages](https://docs.github.com/en/pages).

`https://<nombre_usuario>.github.io/<nombre_repositorio>`

Es necesario configurarlo correctamente siguiendo las instrucciones oficiales, ya sea a través
de la web de [Jekyll](https://jekyllrb.com/docs/) o por las de [Github](https://docs.github.com/en/pages/quickstart).

Dado que los enlaces se construyen de forma distinta en local y en producción, es una posible solución, tener en cuenta los
siguientes puntos para que funcionen en ambos entornos (desarollo-*development* y producción-*production*).

1. Modificar el archivo `_config.yml` con las variables necesarias, especificando las requeridas en producción, concretamente en nuestro ejemplo: `baseurl: /rlstevenson`
```yml
...
domain: rodrom.github.io
url: https://rodrom.github.io
baseurl: /rlstevenson 
...
```

2. Crear un archivo `_config_development.yml` **solo** con las variables necesarias de desarrollo local:
```yml
domain: localhost
url: http://localhost
baseurl: ""
```

3. En cualquier lugar que haya que crear un enlace completo desde la base de sitio, se antepone el valor la variable `baseurl`.
Usando el lenguaje [**Liquid**](https://shopify.github.io/liquid/), que es el que usa este generador de contenido estático,
se podría crear los enlaces de la siguiente forma:

```Liquid
<a href="{{ "{{ site.baseurl " }}}}/about.html">About</a>
```
> **NOTA**: Este código es solo visible correctamente en el sitio en producción generado estáticamente, si lo estás viendo a traves de la página del fichero [markdown original](https://github.com/rodrom/rlstevenson/blob/master/_posts/2023-05-07-github-pages.md) en la web del repositorio Github, te saldrán dos *llaves* `}}` de más.

Que generarían una salida final diferente para el atributo `href` del enlace en función del entorno de ejecución.

Por ejemplo, suponiendo que el usuario de github es: [**rodrom**](https://github.com/rodrom) y el repositorio es [**rlstevenson**](https://github.com/rodrom/rlstevenson), la salida sería:

- Desarrollo: `http://localhost:4000/about.html`
- Producción: `https://rodrom.github.io/rlstevenson/about.html`

Con esta solución, se requiere indicar al arrancar el servidor local que se use el fichero de configuración `_config_development.yml`.

Para ello, basta ejecutar este comando:
`$ jekyll serve --livereload --host=127.0.0.1 --config _config.yml,_config_development.yml`
Que además, te permite ver los cambios de la web cada vez que modificas un archivo.

Hay más información en la página de Jekyll sobre [Environments](https://jekyllrb.com/docs/configuration/environments/), especialmente la opción [`--config`] que se indica al final de la página.

Me despido recomendado la lectura de la historia corta del señor Robert Louis Stevenson.

Os dejo con una cita de su novela *El Dr. Jekyll y Mr. Hyde* de 1886, donde se analiza la **dualidad del individuo**.

> —No, señor —dijo—. No es de un loco. Pero la letra es muy extraña.[0]
>
> ORIGINAL: *“No sir,” he said: “not mad; but it is an odd hand.”*[1]

[\[0\]](https://es.wikisource.org/wiki/El_caso_extra%C3%B1o_del_doctor_Jekyll/V)
[\[1\]](https://www.gutenberg.org/cache/epub/43/pg43-images.html#chap04)