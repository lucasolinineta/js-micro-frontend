# Micro Front End JS

Tener en cuanta que hay varias teorías de como desarrollar micro front, vamos a encontrar diferentes maneras de hacer todos los paso que detallo a continuación.

#### Lo importante es tener en cuenta siempre estos lineamientos generales:

##### Que no haya acoplamiento entre los proyectos hijos
	1.  No import de funciones objetos o clases entre proyectos
	2.  No compartir estado
	3.  Compartir lib mediante module federation esta bien
##### La menor cantidad de acoplamiento entre container y child apps
	1.  El container no debería asumir cada hijo usa algún framework en especial
	2.  Cualquier comunicación necesaria puede hacerse mediante callbacks o eventos simples
##### El css de un proyecto no debe afectar el css de otro
##### Control de versión (monorepo vs separate) no debería tener impacto sobre el resto de los proyectos
	1.  Algunas personas quieren usar monorepo
	2.  Otras personas quieren tener todo por separado
##### El container debería poder decidir siempre si usa la ultima versión del microfront o alguna en específico
	1.  El container va a usar siempre la ultima versión de un microfront, entonces no no requiere redeployar el container
	2.  El container va a usar dif versiones, entonces de deploy
##### No mono repo
##### Una app por cada “Producto” → “XAPP” de ahora en mas
##### Fácil de entender y rápido de modificar

### CONTAINER : como, cuando y donde se renderizar las xapps

#### Integraciones:
	1.  Build-time: container load in browser → xapp render
	2.  Run-time: container load in browser → xapp render
	3.  Server: mientras se envía js para cargar el contenedor, el servidor decide si incluir o no x app. (no voy a hacer desarrollo sobre esta estrategia)

#### BUILD-TIME 
	1.  Desarrollo xApp
	2.  Deploy
	3.  Publicar xapp como NPM
	4.  El equipo de Container incluye las xpps como dependencias
	5.  Container Team construye su propia ap
	6.  Output bundle que incluye todo el código para cada xapp
Pro: setup y comprensión facil
Contra: Cada vez que se modifica xApp se tiene q redeployar el container. Containar y xApp muy acoplados.

#### RUN-TIME
	1.  Desarrollo de xApp
	2.  Deploy En [myapp.com/xapp.js](http://myapp.com/xapp.js)
	3.  El usuario navega en [myapp.com](http://myapp.com), cuando container app ya esta cargada.
	4.  Container app fetch xapp.js a executesit
Pro: Xapp puede ser deployada independientemente En cualquier momento. Diferentes versiones de xapp deployadas y container puede decidir cual usar
Contra: herramientas y setup mas complicados.

### FOCO DE LA GUIA RUN-TIME
##### Comprender setup y herramientas
##### implementación mas flexible y perfomante
##### Foco en webpack

### Estructura de Proyecto

#### Container
	src
		index.js
	public
		index.html
		package.json
		webpack.config.js

#### Products (Cart / Product)
	src
		index.js	
	public
		index.html
		package.json
		webpack.config.js

##### El producto puede ser desarrollado en cualquier framework de js. En este caso de ejemplo sera en js plano
##### El producto puede correr por si solo
##### El producto puede correr a travez del container app

> git clone git@github.com:lucasolinineta/js-micro-frontend.git
> cd js-micro-frontend

#### Recordar que cada XAPP debe correr por si sola, pero el container requiere que las XAPP ya esten corriendo

>cd cart
>npm install
>npm start
>cd ..
Ver http://localhost:8082/
>cd products
>npm install
>npm start
Ver http://localhost:8081/
>cd ..
>cd container
>npm install
>npm start
Ver http://localhost:8080/



