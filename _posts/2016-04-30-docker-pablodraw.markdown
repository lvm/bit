---
slug: 'docker pablodraw'  
title: docker-pablodraw
tags:  
- docker  
- pablodraw  
- ascii  
- o/    
---

Hace alrededor de un mes que estoy utilizando bastante [Docker](https://www.docker.com/) (realmente es *muy* practico) y una de las imagenes que me hice fue para utilizar [PabloDraw](http://picoe.ca/products/pablodraw/), un editor de ANSI/Ascii.  
Considerando que probablemente le resulte util a otras personas, pense en publicarla en  [hub.docker.com](https://hub.docker.com/), sin embargo me encontre con un problema: `Repository does not exist`, para solucionar esto solo necesitamos *taggear* la imagen con el nombre `${user}/${repo}` y listo.  

La imagen la pueden descargar ejecutando:  
```
$ docker pull lvm23/pablodraw
```

y luego:  
```
$ docker run -it -v /tmp/.X11-unix:/tmp/.X11-unix -v /tmp/asc:/asc -e DISPLAY=unix$DISPLAY --name pablodraw pablodraw
```

