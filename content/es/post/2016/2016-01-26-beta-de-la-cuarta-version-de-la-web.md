+++
title = "Beta de la cuarta version de la web"
date = 2016-01-26T13:13:59+01:00
draft = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["drupal", "web", "scrum"]
categories = ["Herramientas Digitales"]
people = ["Autobombo"]

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = "post/captura_de_pantalla_feta_el_2016-01-25_a_les_22.16.04.png"
caption = "Captura de pantalla de la cuarta versión de la web, usando drupal"
preview = true

+++

<p>Quienes conozcan mi web desde hace tiempo y la hayan visitado recientemente habrán notado un cambio profundo en su aspecto, y es que desde el 1 de enero de 2016 hice la <a href="#changelog">cuarta re-estructuración</a> radical de mi sitio web. Aunque visualmente los cambios en apariencia son más que evidentes, los cambios son mucho más profundos: Han pasado ya casi cinco años desde que <a href="/blog/2011/03/08/nuevo-sitio-web-es-lo-mismo-pero-no-es-lo-mismo">en febrero de 2011 decidiese abandonar mis sitios en wordpress y utilizar la recién estrenada versión 7.0 de drupal</a>. Durante este tiempo ha cambiado mucho el panorama: hoy es necesario tener una web con <a href="https://en.wikipedia.org/wiki/Responsive_web_design">Responsive Web Design</a>, Drupal es un proyecto mucho más maduro, y mis circunstancias profesionales y personales han cambiado y debían reflejarse también en el sitio. Por otro lado, hacía ya tiempo que estaba pagando la factura de haber construido un sitio web sin apenas una reflexión o buena planificación detrás (en realidad fue mi primer sitio realizado con drupal 7) y hacía que no estuviera bien optimizada o que en los últimos meses fuese imposible añadir nuevo contenido o editar el existente. Todo ello, sumado al hecho de querer poner en práctica algunas buenas prácticas aprendidas en los últimos años (en especial durante mi etapa en <a href="http://ymbra.com" target="_blank">Ymbra</a>, a la que le debo mucho como drupalero) exigía un cambio profundo que fuese más allá de las actualizaciones de seguridad y pequeños cambios que hacía periódicamente a la web.</p>
<p>Por todo ello, y a pesar de que me resistía a hacerlo por falta de tiempo (que no por falta de ganas), me decidí a hacer una refactorización completa del sitio (esto es, hacerlo de nuevo) y migrar el contenido existente. Pero sin duda, el objetivo principal era que pudiese tener la web operativa y suficientemente atractiva como para volver a escribir en la mayor brevedad posible, así que empiezo predicando con el ejemplo y a continuación detallo algunos de los aspectos que considero más relevantes del cambio.<!--break--></p>
<h3>Replicabilidad y entornos de trabajo</h3>
<p>Una de las cosas buenas que tiene drupal es que además de la separación clásica entre visualización y funcionalidad, también es posible utilizar <a href="http://dgo.to/features" target="_blank">features</a>[fn]Eso en caso de usar Drupal 7, para quienes ya utilicen la recién estrenada Drupal 8, esta funcionalidad se encuentra ya en core y mejorada[/fn] para convertir las configuraciones a código. La utilización de features y perfiles de instalación permite la creación de una <a href="https://www.drupal.org/documentation/build/distributions" target="_blank">distribución de drupal</a> para fines específicos, algo que hacía tiempo quería poner en práctica. De esta forma, si se combina con un sistema de control de versiones como GIT, puede replicarse inmediatamente un sitio web en distintos entornos, sin tener que recurrir a tediosas configuraciones manuales. Si además todo ello se combina con alias de drush se pueden tener copias idénticas de sitios webs a través de comandos en pocos segundos, lo cual es perfecto para desarollar utilizando distintos entornos de desarrollo. En mi caso desarrollo y pruebo en local, y luego lo paso a mi servidor de producción, aunque no descarto utilizar un entorno de pruebas más adelante.</p>
<p>Me hubiese gustado utilizar un workflow con <a href="https://es.wikipedia.org/wiki/Integraci%C3%B3n_continua">integración contínua</a> y probar <a href="https://travis-ci.org/">travis</a> o <a href="https://about.gitlab.com/gitlab-ci/">gitlab ci</a>, pero he tenido que posponerlo debido a la complejidad técnica y a que he querido priorizar el poder empezar a escribir de nuevo con la mayor brevedad posible.</p>

<h3>Migración</h3>
<p>Sin duda esta ha sido la parte más crítica del proyecto. Dado que el sitio web es un sitio nuevo a todos los efectos, no solo era necesario migrar todo el contenido y archivos (mayormente fotos) existentes manteniendo también sus URLS (no querría tener enlaces rotos o perder el SEO que aún me quedase), sino que además, dado que había optimizado los tipos de contenidos unificando tipos[fn]Anteriormente utilizaba tipos de contenidos para fines tan específicos que apenas tenía cuatro entradas en alguno de ellos[/fn] y racionalizando los campos utilizados era necesario mapear cada uno de ellos. Aunque nunca antes había hecho una migración como esta, me sorprendió lo relativamente sencillo (aunque tedioso) que ha sido utilizar los módulos migrate y migrate_d2d. Curiosamente donde he sufrido más ha sido en la migración de comentarios, pues aunque pensaba que utilizar un servicio externo como disqus me facilitaría enormemente la tarea (siempre que mantuviese los paths, algo que hice), la realidad ha sido la contraria y la <a href="https://www.drupal.org/node/2654034" target="_blank">solución que he utilizado</a> finalmente es algo chapucera.</p>

<h3>Workflow</h3>

<p>Sin duda uno de los mayores cambios a nivel técnico no se ha producido en la web en si sino en mi forma de trabajar, y es que he querido adaptar un sistema de trabajo similar al utilizado en Ymbra con el que me he sentido tan a gusto (teniendo en cuenta que trabajo solo y que por tanto habrá cosas que no tienen sentido hacer). Básicamente el gran cambio es que en lugar de empezar a desarrollar lo que me apetezca en cada momento, antes de tocar drupal creo una issue en <a href="https://gitlab.com">gitlab</a> [fn]Cambiar de plataforma ha sido otro de los cambios: anteriormente utilizaba bitbucket, pero <a href="https://gitlab.com">gitlab</a> me enamoró desde el principio, pues además de permitir tener repositorios privados de forma gratuita, o tener una interfaz de usuario muy agradable, ofrece funcionalidades muy interesantes que van más allá de los que ofrece bitbucket. Por suerte, dado que git es distribuido, cambiar de plataforma fue tan sencillo como añadir un nuevo remoto a git.[/fn] que trato de redactar como historia de usuario o bien como historia técnica[fn]Ver la <a href="/blog/2014/05/21/sesion-drupalcamp-spain-2014-scrum-una-retrospectiva">sesión de Scrum que presenté en la DrupalcampSpain de Valencia</a>[/fn] y posteriormente agrupo y priorizo cada issue en varias milestones con objetivos concretos. Puede que parezca un proceso tedioso o que no tenga mucho sentido utilizar si se trabaja solo, pero mi experiencia ha sido tremendamente positiva ya que tiene las siguientes ventajas:</p>
<ol><li>Siempre tengo claro lo que tengo que hacer, incluso cuando pasan largos periodos de tiempo entre desarrollo y desarrollo.</li><li>Es una excelente forma de consulta. Aunque pueda sonar un poco enfermizo, las "conversaciones" que tengo con mi mismo en las issues, aportando documentación o comentarios, son una ayuda excelente para que no olvide nada y no pierda tiempo buscando información cada vez que intento solucionar algo.</li><li>Cada commit de git está asociado a una issue de gitlab, con lo cual se puede relacionar el log de git con cada issue y viceversa, facilitando el seguimiento del estado de una tarea y haciendo facil la opción de revertir cualquier cambio en caso necesario.</li><li>Utilizar estos métodos, hablarme en inglés... aunque no sean muy naturales son una forma de no perder "estado de forma", para el día en el que vuelva a trabajar en equipo.</li><li>Permite un sistema de desarrollo iterativo (ver a continuación).</li></ol>

<h3>Proyecto mínimo viable y desarrollo iterativo</h3>
<p><img alt="" src="/img/post/captura_de_pantalla_feta_el_2016-01-25_a_les_23.12.02.png" title=""></p>

<p>Como comentaba anteriormente, la reestructuración del site se debía a dos objetivos principales: por un lado poder volver a escribir (apenas escribí nada durante 2015 y eso se debió en gran parte -aunque no exclusivamente- a problemas técnicos), y por otro tener un sitio que mejorase considerablemente a nivel técnico. El problema es que hay tanto por mejorar que, de querer tener resueltos todos los aspectos que quiero desarrollar, me demoraría tanto (especialmente si tenemos en cuenta mi tiempo limitado) que no haría posible cumplir con el primer objetivo. Por todo ello, y gracias al sistema de trabajo utilizado que he descrito anteriormente, decidí salir con un <a href="http://en.wikipedia.org/wiki/Minimum_viable_product" target="_blank">producto mínimo viable</a> que que diese respuesta a las necesidades más básicas al que iría añadiendo mejoras de forma incremental. Una vez asumido que el sitio estará en un estado de casi-beta-permanente, lo demás todo son buenas noticias: con el tiempo se irán viendo las novedades y yo no me agobiaré por tenerlo todo listo a pesar de mi poco tiempo para desarrollarlo.</p>
<h3>Theme responsive</h3>
<p>He optado por utilizar un subtema de <a href="http://dgo.to/zen" target="_blank">Zen</a> que sea responsive y en el que haya pocos elementos gráficos y prime la facilidad de lectura. De momento, aunque es operativo, es todavía muy mejorable. Todo se andará. Eso sí, el color naranja se mantiene ;)</p>
<p>------------------------</p>
<p>Lo que sigue a continuación es información para friquis/entusiastas (puedes saltar directamente a los <a href="#disqus_thread">comentarios</a>:</p>
<p><a id="changelog" name="changelog"></a>+++CHANGELOG+++</p><p><strong>2016/01/01: v.4.0-beta1</strong><br>-------------------------</p><ul><li>Re-factorización completa de un sitio web en drupal 7 aplicando features y perfiles de instalación.</li><li>Migración de contenido</li><li>Theme responsive creado desde cero (subtheme de Zen)</li></ul><p>&nbsp;</p><p><strong>2011/03/08:</strong> <strong>v3.0</strong><br>-------------------------</p><p>Migración de los dos wordpress (blog y web curricular) a una sola instalación de drupal.<br>Cambio de arquitectura, diseño y funcionalidades de la web.</p><ul><li>Gestor: Drupal 7 (una sola instalación para blog, web curricular y lo que se preste )</li><li>Diseño: plantilla provisional modificada a partir de la plantilla Bartik</li></ul><p>&nbsp;</p><p><strong>2008/12/??:</strong> <strong>v2.1</strong><br>-------------------------</p><p>cambio ligero en el diseño y creación de otro blog instalado en la raiz del dominio para gestionar únicamente aspectos curriculares, utilizando exactamente la misma apariencia gráfica que el blog existente.<br>Este sistema surgía de la dificultad de mantener actualizado mi CV con la página HTML ya que permitía tener uno fácilmente actualizable, tal y como ya hacía con el blog.</p><ul><li>Gestor: dos instalaciones independientes de Wordpress 2.7, una para el blog y otra para la web curricular</li><li>Diseño: Plantilla modificada ligeramente para<ul><li>aprovechar nuevos widgets</li><li>ampliación del ancho de sidebar derecho</li><li>se añade botones de compartir en la red</li></ul></li></ul><p><strong>2007/12/??:</strong> <strong>v2.0</strong><br>-------------------------</p><p>migración de carloscamara.es al gestor de contenidos Wordpess en una subcarpeta "/blog".<br>Utilización de wordpress para gestionar el blog, enlaces a otras webs, categorizar entradas... se mantiene el sitio HTML en la raiz del sitio para la web curricular.</p><ul><li>Gestor: Wordpress 2.0 "Duke" (blog)</li><li>HTML para web curricular (sigue sin alteraciones)</li><li>Misma plantilla CSS (sigue sin alteraciones)</li></ul><p><strong>2006/12/03:</strong> <strong>v1.0</strong><br>-------------------------</p><p>Creación de un sitio web en HTML que combina la integración de un blog realizado en Blogger con la misma plantilla gráfica.<br>Este método permitía tener un sitio dinámico que permitiese comentarios y actualizaciones constantes conuna misma apariencia gráfica y sin tener conocimientos de programación.</p><ul><li>Gestor: Blogger (blog)</li><li>HTML para web curricular</li><li>Misma plantilla CSS</li></ul><p><strong>2006/05/??:</strong> <strong>v0.1</strong><br>-------------------------</p><p>Tras la experiencia de haber desarrollado +arquitectura y gracias al empujón de una iniciativa del Ministerio de Industria para que los españoles podamos tener un dominio .es a 1€, nace carloscamara.es como excusa para profundizar en el aprendizaje de HMTL y CSS y para tener un blog propio.</p>