---
slug: 'arte-electronico'  
title: Arte Electrónico argentino  
tags:  
- docker  
- golang  
- gin  
- gorp  
- node  
- emberjs  
- travis-ci  
- arte  
---


# Creando un sitio de "Arte Electrónico argentino"

Hace unas semanas vi que [Cristian Reynaga](http://cristianreynaga.com/) había publicado un [Dataset de Arte Electrónico argentino](https://github.com/cristianReynaga/Dataset-Arte-Electronico-Argentino) que utilizo para un [documental](https://vimeo.com/76021448) que estaba realizando, por lo que me pareció una buena idea armar una aplicación que permitiese consultar estos datos de una manera cómoda.

## Interfaces para desarrolladores

Para llevar a cabo esta tarea decidí utilizar [Golang,](https://golang.org/) un lenguaje desarrollado por Robert Griesemer, Rob Pike y Ken Thompson. Las razón? simplemente hacia tiempo un amigo hablo maravillas del lenguaje y quise darle una oportunidad haciendo un proyecto *serio*. Por supuesto que no lo escribí de cero, sino que utilice [Gin-gonic,](https://gin-gonic.github.io/gin/) un framework web hecho en este lenguaje.
Del sitio del framework:
> Gin is a web framework written in Go (Golang). It features a martini-like API with much better performance, up to 40 times faster thanks to [httprouter](https://github.com/julienschmidt/httprouter). If you need performance and good productivity, you will love Gin.

En efecto. No solo es rápido como aplicación, además permite escribir aplicaciones web (en este caso una API RESTful) en muy poco tiempo, inclusive para gente como yo que viene de otros lenguajes como Python (interpretado, de tipado dinámico, a diferencia de Golang que es compilado y de tipado estático). Adicionalmente utilice [Gorp](https://github.com/go-gorp/gorp), un ORM*-ish* para facilitarme la vida con las consultas.

En cuestión de unos días le di formato al CSV para poder importarlo sin mayores problemas a una base de datos en SQLite, arme al prototipo inicial (*v1*), generé un contenedor de [Docker](https://www.docker.com/) para su *deployment* y estaba publicado y funcionando.

La aceptación de la gente también fue bastante positiva, por lo que hasta ahora se puede hacer un balance bastante positivo de una aplicación escrita en tres días para probar un lenguaje :-)

Por supuesto, el código de la API está disponible en [Github](https://github.com/lvm/api-dataset-arte-electronico-argentino).

##Interfaces para *humanos*

A pesar de que la API estaba funcionando bien y había tenido buena aceptación, aquellos que no están familiarizados con consultar datos haciendo *requests *y *parseando* estos resultados, realmente no iban a poder hacer uso de esta información por lo que me puse a hacer la pata restante: Un front-end para directamente visualizar los datos.

En este caso utilicé [Ember.js,](http://emberjs.com/) un framework en JavaScript para *aplicaciones web ambiciosas*. Sobre este framework no tengo demasiado para decir, excepto que me parece **mucho** mas cómodo que [Angular](https://angularjs.org/) y mas completo que React.js (que del modelo MVVM, solo cuenta con la **V**iew), por lo que no lo pensé demasiado al elegir uno.
Para comenzar el proyecto, en lugar de instalar [ember-cli](https://ember-cli.com/) directamente en mi computadora, elegi utilizar al contenedor de Docker [danlynn/ember-cli](https://github.com/danlynn/ember-cli) junto con [ember-blueprint](https://github.com/frank06/ember-blueprint) y en unos instantes tenia un *esqueleto* listo para desarrollar la aplicación.

Nuevamente, gracias a la excelente documentación de [Ember.js,](http://emberjs.com/) en cuestión de dias tenia al sitio web listo para publicar, inclusive con un diseño *relativamente decente *:-)

En este caso el código también está disponible en [Github](https://github.com/lvm/site-dataset-arte-electronico-argentino).

##Automatizando tareas

*o ¿Por que realizar manualmente tareas que se pueden hacer solas?*

***Deployando* con Docker Hub**

En el caso de la API, simplemente fue necesario crear la [*receta](https://github.com/lvm/api-dataset-arte-electronico-argentino/blob/master/Dockerfile) *para generar al binario que haría las veces de *servidorcito* utilizando la [imagen oficial de Golang](https://hub.docker.com/_/golang/) como base.
Teniendo todo listo, simplemente asocié mi cuenta de Github en [Docker Hub](http://hub.docker.com/) y cree un [Automated Build](https://hub.docker.com/r/lvm23/api-arte-electronico-argentino/) que, si todo funciona correctamente, nos genera una imagen lista para descargar y ejecutar:
> docker pull lvm23/api-arte-electronico-argentino

**Integración continua con Travis**

Por el otro lado, si bien [Ember.js](http://emberjs.com/) es super genial, necesitamos compilar la aplicación para poder *servirla* como cualquier sitio *estático *y que mejor que [Travis-CI](https://travis-ci.org/) para llevar a cabo esta tarea?
En este caso, fue necesario crear un archivo [*.travis.yml](https://github.com/lvm/site-dataset-arte-electronico-argentino/blob/master/.travis.yml) *junto con un [script](https://github.com/lvm/site-dataset-arte-electronico-argentino/blob/master/deploy-to-ghpages.sh) que ejecuten las acciones necesarias para *deployar* nuestra aplicación y publicar automáticamente en Github Pages al crear un nuevo tag (de otro modo, con cada *push* se generaria un nuevo build).

##En resumen

En cuestión de una semana pude desarrollar un sitio desde *atrás* hacia *adelante* con herramientas súper prácticas con la idea de poder facilitar el acceso a la información y que sirva de referencia para futuros proyectos :-)

##Hipervinculos relacionados

* [Sitio de Arte Electrónico argentino](http://arte-electronico.cyberpunk.com.ar/)

* [API pública de Arte Electrónico argentino](http://api.arte-electronico.cyberpunk.com.ar/)

* [Dataset del sitio](https://github.com/cristianReynaga/Dataset-Arte-Electronico-Argentino)

* [Código del FrontEnd del sitio](https://github.com/lvm/site-dataset-arte-electronico-argentino)

* [Código del BackEnd del sitio](https://github.com/lvm/api-dataset-arte-electronico-argentino)

* [Contenedor de Docker del BackEnd del sitio](https://hub.docker.com/r/lvm23/api-arte-electronico-argentino/)

* [Builds del FrontEnd del sitio](https://travis-ci.org/lvm/site-dataset-arte-electronico-argentino)
