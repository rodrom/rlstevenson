---
title: "Configurar Github Pages de un repositorio como éste"
author: rodrom
---

Recién iniciado el séptimo día del mes quinto del duomilésimovigésimotercer ciclo
del tercer planeta del sistema solar en el horario de Europa Occidental Central,
he conseguido, creo, averiguar que se necesita para configurar correctamente
los enlaces, relativos o absolutos, de una web **Jekyll** usando como hosting el servicio
*gratuito* de Github, propiedad de Microsoft.

Ignoro porque le han dado este nombre de *Jekyll*, ¿quizás tenga que ver con que Internet,
al igual que en la novela del escritor nacido ayer, 6 de mayo, **Robert Louis Stevenson**,
en *Dr. Jekyll y Mr. Hyde*, es como una pócima que saca lo peor de si mismos a algunos humanos?
Ni idea. No conozco al señor que creo que este programa para aumentar el ego de escritores
fracasados, o no.

El caso es que, si 
1. Configuras un entorno de desarrollo para *Jekyll*,
  + instalar *ruby*
  + instalar *bundle* y *jekyll*
2. Creas una serie páginas y entradas de forma que te funciona en local
3. Inicias un repositorio Git
4. Lo subes a Github a un repositorio remoto de nombre arbitrario, como en mi caso *rlstevenson*.
  + Activas la opción de sea una *Github Page* y configuras los parámetros.
  + Esperas a que se ejecute la acción por defecto de *Github Actions*
  + Y con suerte todo funciona.
  + Tu proyecto ya está disponible en `https://<tu-usuario>.github.io/<el-nombre-del-repositorio>`.
  
Es probable que haya un conflicto entre los enlaces que se generan en la versión de desarrollo local y los que se deberían mostrar
en la versión en producción. Por ejemplo:
Está página, que forma parte de una entrada de mi cuaderno de bitácora, que en inglés se dice *blog post* es:
- Enlace en local: `http://localhost:4000/2023/05/07/github-pages.html`
- Enlace en producción: `https://rodrom.github.io/rlstevenson/2023/05/07/github-pages.html`.

La clave está en meter la parte de `rlstevenson` solo en producción, pero ignorarla, en local.

He estado mirando varias páginas en Internet, esa que a veces saca cosas buenas, y otras es una perdida constante de tiempo.
Los términos de producción y local, la verdad que están elegidos, malamente. Pero no seré yo el que cambié los términos de esta,
relativamente, pseudo ciencia/ingeniería/... y su jerga. Y el caso es, que no he encontrado una solución sencilla. He probado varias cosas
hasta que he llegado a la siguiente solución:

1. Crear un archivo `_config.yml` con las variables necesarias de producción: `baseurl: /rlstevenson`
2. Crear un archivo `_config_development.yml` con las variables necesarias de desarrollo local: `baseurl: ""`
3. En cualquier lugar que haya que crear un enlace absoluto, se antepone el valor de dicha variable.
    Usando el lenguaje `Liquid`, que es el que usa este generador de contenido estático, se podría crear los enlaces de la siguiente forma:

```txt
{{ "{{ site.baseurl " }}}}/about.html
```

Que generarían una salida final dependiente del entorno de ejecución:

- Desarrollo: `http://localhost:4000/about.html`
- Producción: `https://rodrom.github.io/rlstevenson/about.html`

Con esta solución, se requiere indicar al arrancar el servidor local que se use el fichero de configuración `_config_development.yml`
Para ello basta ejecutar este comando: 
`$ jekyll serve --livereload --host=127.0.0.1 --config _config_development.yml`

Y con esto y un bizcocho, hasta mañana a las ocho. Que puede que retoque algo el texto. O no. La verdad que soy poco de revisar.
Pero puede que con esto haga una excepción.

Espero que con esta lectura te hayan entrado ganas de leer a Robert Louis Stevenson,
porque el tío escribe bastante mejor que yo y que tú.

Os dejo con una cita de su novela *El Dr. Jekyll y Mr. Hyde* de 1886, donde se analiza la **dualidad del individuo**.
Y creo que no se refería al móvil, ni al trastorno bipolar de algunos individuos.

> [Henry Jekyll]
> —No, señor —dijo al final—. No está loco. Pero tiene una caligrafía muy extraña.