# Motivación

Como los requisitos en aplicaciones JavaScript de una sola página se están volviendo cada vez más complicados, **nuestro código, mas que nunca, debe manejar el estado**. Este estado puede incluir respuestas del servidor y datos cacheados, así como datos creados localmente que todavía no fueron guardados en el servidor. El estado de las UI también se volvió más complejo, al necesitar mantener la ruta activa, el tab seleccionado, si mostrar o no un spinner, si deben mostrarse los controles de paginación o no.

Controlar ese cambiante estado es difícil. Si un modelo puede actualizar otro modelo, entonces una vista puede actualizar un modelo, el cual actualiza otro modelo, y esto causa que otra vista se actualice. En cierto punto, ya no se entiende qué esta pasando en la aplicación ya que **perdiste control sobre el cuándo, el por qué y el cómo de su estado**. Cuando un sistema es opaco y no determinista, es difícil reproducir errores o agregar nuevas características.

Como si no fuera suficientemente malo, considera que **los nuevos requisitos son comunes en el desarrollo front-end**. Como desarrolladores, se espera que manejemos actualizaciones, renderizado en el servidor, obtener datos antes de realizar cambios de rutas, y más cosas. Nos encontramos tratando de controlar algo más complejo que nunca, e inevitablemente nos preguntamos: [es tiempo de rendirse?](http://www.quirksmode.org/blog/archives/2015/07/stop_pushing_th.html) La respuesta es _no_.

Esta complejidad es difícil de manejar debido a que **estamos mezclando dos conceptos** que son difícil de entender para la mente humana: **mutaciǿn y asincronicidad**. Les llamo [Mentos y Coca-Cola](https://en.wikipedia.org/wiki/Diet_Coke_and_Mentos_eruption). Ambos son geniales separados, pero juntos pueden causar un gran lío. Librerías como [React](http://facebook.github.io/react) tratan de resolver este problema en la capa de la vista removiendo tanto la asincronicidad como la manipulación directa del DOM. De todas formas, controlar el estado de tus datos es todavía tu responsabilidad. Acá es donde entra Redux.

Siguiendo los pasos de [Flux](http://facebook.github.io/flux), [CQRS](http://martinfowler.com/bliki/CQRS.html) y [Event Sourcing](http://martinfowler.com/eaaDev/EventSourcing.html), **Redux intenta hacer predecibles las mutaciones del estado** imponiendo ciertas restricciones en cómo y cuándo pueden realizarse las actualizaciones. Estas restricciones se reflejan en los [tres principios](./tres-principios.md) de Redux.