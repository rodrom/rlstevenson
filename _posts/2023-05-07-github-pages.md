---
title: "Configurar Github Pages de un repositorio como este"
author: rodrom
---

Recién iniciado el séptimo día del mes quinto del duomilesimo y vigésimotercer ciclo
del tercer planeta del sistema solar en el horario de Europa Occidental Central,
he conseguido, creo, que se necesita para configurar correctamente
los enlaces, relativos o absolutos, de una web [**Jekyll**}(https://jekyllrb.com),
usando como hosting el servicio *gratuito* de [Github Pages](https://pages.github.com/), propiedad de Microsoft.

Ignoro porque le han dado este nombre de *Jekyll*, ¿quizás tenga que ver con que Internet,
al igual que en la novela del escritor nacido ayer, 6 de mayo, [**Robert Louis Stevenson**](https://es.wikipedia.org/wiki/Robert_Louis_Stevenson),
en [*Dr. Jekyll y Mr. Hyde*](https://www.gutenberg.org/ebooks/43), es como una pócima que saca lo peor de si mismos a algunos humanos?
Ni idea. No conozco al señor, [Tom Preston Werner](https://tom.preston-werner.com/), que no creo que diseñase este programa para aumentar el ego de escritores
fracasados.

Si sigues las [instrucciones de instalación oficiales](https://jekyllrb.com/docs/installation/) 
1. Configuras un entorno de desarrollo para *Jekyll*,
  + instalar *ruby*
  + instalar *bundle* y *jekyll*
2. Creas una serie páginas y entradas de forma que te funciona en local
3. Inicias un repositorio Git
4. Lo subes a Github a un repositorio remoto de nombre arbitrario, como en mi caso [*rlstevenson*](https://github.com/rodrom/rlstevenson).
  + Activas la opción de sea una [*Github Page*](https://docs.github.com/en/pages) y configuras los parámetros.
  + Esperas a que se ejecute la acción por defecto de *Github Actions*
  + Y con suerte todo funciona.
  + Tu proyecto ya está disponible en `https://<tu-usuario>.github.io/<el-nombre-del-repositorio>`. O en mi caso: [](https://rodrom.github.io/rlstevenson)
  
Es probable, que haya un conflicto entre los enlaces que se generan en la versión de desarrollo local y los que se deberían mostrar en producción.

Por ejemplo:
Está página, que forma parte de una entrada de mi cuaderno de bitácora, que en inglés se dice *blog post* es:
- Enlace en local: `http://localhost:4000/2023/05/07/github-pages.html`
- Enlace en producción: `https://rodrom.github.io/rlstevenson/2023/05/07/github-pages.html`.

La clave está en meter la parte de `rlstevenson` solo en producción, pero ignorarla, en local.

He estado mirando varias páginas en Internet, esa que a veces saca cosas buenas, y otras es una perdida constante de tiempo.
Los términos de producción y local, la verdad que están elegidos, malamente. Pero no seré yo el que cambié los términos de esta,
relativamente, pseudo ciencia/ingeniería/... y su jerga. Y el caso es, que no he encontrado una solución clara y seniclla. He probado varias cosas, hasta que he llegado a la siguiente solución:

1. Crear un archivo `_config.yml` con las variables necesarias de producción: `baseurl: /rlstevenson`
2. Crear un archivo `_config_development.yml` con las variables necesarias de desarrollo local: `baseurl: ""`
3. En cualquier lugar que haya que crear un enlace absoluto, se antepone el valor de dicha variable.
    Usando el lenguaje `Liquid`, que es el que usa este generador de contenido estático, se podría crear los enlaces de la siguiente forma:

```txt
{{ "{{ site.baseurl " }}}}/about.html
```
>> **NOTA**: Este código es solo visible correctamente en el sitio en producción generado estáticamente, si lo estás viendo a traves de la página del fichero markdown original en la web del repositorio Github, te saldrán dos *llaves* `}}` de más.

Que generarían una salida final dependiente del entorno de ejecución:

- Desarrollo: `http://localhost:4000/about.html`
- Producción: `https://rodrom.github.io/rlstevenson/about.html`

Con esta solución, se requiere indicar al arrancar el servidor local que se use el fichero de configuración `_config_development.yml`.

Para ello, basta ejecutar este comando: 
`$ jekyll serve --livereload --host=127.0.0.1 --config _config_development.yml`

Espero que con esta lectura te hayan entrado ganas de leer a Robert Louis Stevenson,
porque el tío escribe bastante mejor que yo y que tú.

Os dejo con una cita de su novela *El Dr. Jekyll y Mr. Hyde* de 1886, donde se analiza la **dualidad del individuo**.
Y creo que no se refería al móvil, ni al trastorno bipolar o maniacodepresivo de algunos.

>> [Henry Jekyll]
>> 
>> —No, señor —dijo—. No es de un loco. Pero la letra es muy extraña.[0]
>>
>> ORIGINAL: *“No sir,” he said: “not mad; but it is an odd hand.”*[1]

[\[0\]](https://es.wikisource.org/wiki/El_caso_extra%C3%B1o_del_doctor_Jekyll/V)
[\[1\]](https://www.gutenberg.org/cache/epub/43/pg43-images.html#chap04)
