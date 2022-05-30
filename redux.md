# <a href='http://es.redux.js.org'><img src='https://camo.githubusercontent.com/f28b5bc7822f1b7bb28a96d8d09e7d79169248fc/687474703a2f2f692e696d6775722e636f6d2f4a65567164514d2e706e67' height='60'></a>

Redux es un contenedor predecible del estado de aplicaciones JavaScript.

Te ayuda a escribir aplicaciones que se comportan de manera consistente, corren en distintos ambientes (cliente, servidor y nativo), y son fáciles de probar. Además de eso, provee una gran experiencia de desarrollo, gracias a [edición en vivo combinado con un depurador sobre una línea de tiempo](https://github.com/gaearon/redux-devtools).

Puedes usar Redux combinado con [React](https://facebook.github.io/react/), o cualquier otra librería de vistas. Es muy pequeña (2kB) y no tiene dependencias.



## Influencias
Redux evoluciona las ideas de [Flux](http://facebook.github.io/flux/), pero evitando su complejidad tomando cosas de [Elm](https://github.com/evancz/elm-architecture-tutorial/).

Ya sea que los hayas usado o no, solo toma unos minutos para empezar a usar Redux.

## Instalación
Para instalar la versión estable:
```bash
npm i -S redux
```
Normalmente también vas a querer usar la [conexión a React](https://github.com/rackt/react-redux) y las [herramientas de desarrollo](https://github.com/gaearon/redux-devtools).
```bash
npm i -S react-redux
npm i -D redux-devtools
```
Esto asumiendo que estás usando [npm](https://www.npmjs.com/) como administrador de paquetes con un empaquetador de módulos como [Webpack](http://webpack.github.io/) o [Browserify](http://browserify.org/) para usar [módulos de CommonJS](http://webpack.github.io/docs/commonjs.html).

Si todavía no usas [npm](https://www.npmjs.com/) o algún empaquetador de módulos moderno, quizás prefieras el paquete en [UMD](https://github.com/umdjs/umd) que define `Redux` como un objeto global, puedes usar una desde [cdnjs](https://cdnjs.com/libraries/redux). *No* recomendamos este enfoque para ninguna aplicación seria, ya que la mayoría de las librerías complementarias a Redux están solo disponibles en [npm](https://www.npmjs.com/).

## El Gist
Todo el estado de tu aplicación está almacenado en un único árbol dentro de un único *store*.
La única forma de cambiar el árbol de estado es emitiendo una *acción*, un objeto describiendo que ocurrió.

Para especificar cómo las acciones transforman el árbol de estado, usas *reducers* puros.

¡Eso es todo!

```javascript
import { createStore } from 'redux';

/**
 * Esto es un reducer, una función pura con el formato
 * (state, action) => newState. Describe como una acción transforma el estado
 * en el nuevo estado.
 *
 * La forma del estado depende de tí: puede ser un primitivo, un array, un
 * objeto, o incluso una estructura de datos de Immutable.js. La única parte
 * importante es que no debes modificar el objeto del estado, en vez de eso
 * devolver un nuevo objeto si el estado cambió.
 *
 * En este ejemplo, usamos `switch` y strings, pero puedes usar cualquier forma
 * que desees si tiene sentido para tu proyecto.
 */
function counter(state = 0, action) {
  switch (action.type) {
  case 'INCREMENT':
    return state + 1;
  case 'DECREMENT':
    return state - 1;
  default:
    return state;
  }
}

// Creamos un store de Redux almacenando el estado de la aplicación.
// Su API es { subscribe, dispatch, getState }.
let store = createStore(counter);

// Puedes suscribirte manualmente a los cambios, o conectar tu vista
// directamente
store.subscribe(() => {
  console.log(store.getState())
});

// La única forma de modificar el estado interno es despachando acciones.
// Las acciones pueden ser serializadas, registradas o almacenadas luego para
// volver a ejecutarlas.
store.dispatch({ type: 'INCREMENT' });
// 1
store.dispatch({ type: 'INCREMENT' });
// 2
store.dispatch({ type: 'DECREMENT' });
// 1
```

En vez de modificar el estado directamente, especificas las modificaciones que quieres que ocurran con objetos planos llamados *acciones*. Entonces escribes una función especial llamada *reducer* que decide como cada acción transforma el estado de la aplicación.

Si vienes de Flux, hay una única diferencia importante que necesitas entender. Redux no tiene Dispatcher ni soporta múltiples stores. En cambio, hay un único store con una única función reductora. Cuando tu aplicación crezca, en vez de agregar más stores, divides tu reducer principal en varios reducers pequeños que operan de forma independiente en distintas partes del árbol de estado. Esto es exactamente como si solo hubiese un componente principal en una aplicación de React, pero está compuesta de muchos componentes pequeños.

Esta arquitectura puede parecer una exageración para una aplicación de contador, pero lo hermoso de este patrón es lo bien que escala en aplicaciones grandes y complejas. También permite herramientas de desarrollo muy poderosas, ya que es posible registrar cada modificación que las acciones causan. Podrías registrar la sesión de un usuario y reproducirlas simplemente ejecutando las mismas acciones.



## Documentación
- [Introducción](docs/introduccion/README.md)
- [Básico](docs/basico/README.md)
- [Avanzado](docs/avanzado/README.md)
- [Recetas](docs/recetas/README.md)
- [Solución de problemas](docs/solucion-de-problemas.md)
- [Glosario](docs/glosario.md)
- [Referencia API](docs/api/README.md)

## Ejemplos
- [Contador](https://github.com/rackt/redux/tree/master/examples/counter)
- [TodoMVC](https://github.com/rackt/redux/tree/master/examples/todomvc)
- [Todos con Deshacer](https://github.com/rackt/redux/tree/master/examples/todos-with-undo)
- [Asíncrono](https://github.com/rackt/redux/tree/master/examples/async)
- [Universal](https://github.com/rackt/redux/tree/master/examples/universal)
- [Mundo real](https://github.com/rackt/redux/tree/master/examples/real-world)
- [Carrito de compra](https://github.com/rackt/redux/tree/master/examples/shopping-cart)
- [Vista de árbol](https://github.com/rackt/redux/tree/master/examples/tree-view)

Si eres nuevo en el ecosistema de NPM y tienes problemas iniciando un proyecto, o no estás seguro de donde pegar el gist de arriba, revisa [simples-redux-example](https://github.com/jackielii/simplest-redux-example) que usa Redux junto a React y Browserify.

## Discusiones
Únete al canal [#redux](https://discord.gg/0ZcbPKXt5bZ6au5t) de la comunidad en Discord [Reactiflux](http://www.reactiflux.com/).

## Agradecimientos
- [The Elm Architecture](https://github.com/evancz/elm-architecture-tutorial) por una gran introducción al modelo de actualización de estado con reducers;
- [Turning the database inside-out](http://www.confluent.io/blog/turning-the-database-inside-out-with-apache-samza/) por explotarme la mente;
- [Developing ClojureScript with Figwheel](https://www.youtube.com/watch?v=j-kj2qwJa_E) por convencerme que la re-evaluaciǿn debe "simplemente funcionar";
- [Webpack](https://github.com/webpack/docs/wiki/hot-module-replacement-with-webpack) por Hot Module Replacement;
- [Flummox](https://github.com/acdlite/flummox) por enseñarme un enfoque a Flux sin boilerplate or singletons;
- [disto](https://github.com/threepointone/disto) por la prueba de concepto de hot reloadable Stores;
- [NuclearJS](https://github.com/optimizely/nuclear-js) por probar que esta arquitectura puede tener buen rendimiento;
- [Om](https://github.com/omcljs/om) por popularizar la idea de un único Store;
- [Cycle](https://github.com/cyclejs/cycle-core) por demostrar que tan común una función puede ser la mejor herramienta;
- [React](https://github.com/facebook/react) por la innovación pragmática.

Agradecimientos especiales a [Jamie Paton](http://jdpaton.github.io/) por liberar `redux` como nombre de módulo en NPM.

## Registro de cambios
Este proyecto se adhiere al [Versionamiento Semántico](http://semver.org/).

Cada lanzamiento, junto a sus instrucciones de migración, están documentados en la página de Github de [Lanzamientos](https://github.com/rackt/redux/releases).

## Patrocinadores
El trabajo con Redux fue [financiado por la comunidad](https://www.patreon.com/reactdx).

Algunos de las compañías más destacadas que hicieron esto posible:

- [Webflow](https://github.com/webflow)
- [Chess iX](http://www.chess-ix.com/)

[Ve la lista completa de patrocinadores de Redux.](docs/PATRONS.md)

## Licencia
MIT
