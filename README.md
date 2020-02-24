> El siguiente contenido fue elaborado por [@_nhsz](https://twitter.com/_nhsz) como guía para las clases de [undefined school](https://twitter.com/undefinedSchool)
> Son bienvenidos los _issues_ y _PRs_ para mejorar el contenido, corregir errores, etc. 

> 👉 Si te resultó útil, **se agradece que lo compartas para que le llegue a más gente!**

# React: Conceptos Básicos

## Notas sobre React

- [**React: Principios**](https://github.com/undefinedschool/notes-react-principles/)
- [**React: Conceptos Básicos**](https://github.com/undefinedschool/notes-react-basics)

## Contenido

---

## React Component

**Un componente es un bloque de código reutilizable e independiente**, una pieza de UI con contenido, estilos y comportamiento definidos.

En React, cada parte de la UI es un componente y cada componente tiene un [estado](https://github.com/undefinedschool/notes-react-basics#state).

Idealmente, [cada componente debería encargarse de una sola cosa](https://en.wikipedia.org/wiki/Single_responsibility_principle). Si crece demasiado, puede a su vez dividirse en _sub-componentes_. Es decir, aplicamos el mismo criterio que utilizamos a la hora de crear funciones u objetos en general.

> 👉 **La UI de nuestra aplicación va a terminar estando definida entonces como un [_árbol de componentes_](https://reactjs.org/docs/thinking-in-react.html#step-1-break-the-ui-into-a-component-hierarchy)**

## Props

Los [componentes](https://github.com/undefinedschool/notes-react-basics#react-component) reciben valores a través de diferentes parámetros a los que llamamos _props_ (por propiedades) y retornan el código necesario (usando [_JSX_](https://github.com/undefinedschool/notes-react-basics#jsx)) para renderizar los componentes. 

Podríamos decir que funcionan de forma similar a los _atributos HTML_, sólo que, en este caso, escribimos JSX en lugar de HTML y las _props_ puede ser cualquier expresión válida en JS. Estos valores (_props_) podrán ser luego utilizados por el componente o pasados a un _child component_.

> 👉 **Las _props_ son inmutables y siempre se pasan de componentes superiores a componentes inferiores<sup>1</sup>**, dicho de otra forma, desde un componente padre (_parent component_) hacia un componente hijo (_child component_).

## State

Un [componentes](https://github.com/undefinedschool/notes-react-basics#react-component) puede simplemente recibir [_props_](https://github.com/undefinedschool/notes-react-basics#props) y renderizarse. 

Por otro lado, los componentes también poseen un _state_, un objeto de JavaScript que se utiliza para almacenar información (características propias) acerca del componente y que puede cambiar a lo largo del tiempo. Estos cambios suelen ser resultado de diferentes eventos producidos por los usuarios (input en un formulario, click sobre un elemento, etc) o el sistema (obtener el resultado de hacer un request a una API, etc).

El _state_ se crea dentro del componente, usando el constructor, para setear su valor inicial (el cual también puede obtenerse a partir de las _props_ que reciba el componente).

```js
constructor() {
  super();
  
  this.state = {
    count: 0,
  };
}
```

El _state_ se va a utilizar entonces para _interactividad_, es decir, datos que cambian a través del tiempo.

> 👉 Recordermos que **la vista es una función del estado**: cuando el estado cambia, la vista se vuelve a renderizar. Por lo tanto, si queremos que la vista (UI) sea actualice, tenemos que modificar el estado de alguna forma.

## Props vs State

Tanto las _props_ como el _state_ tienen características comunes:

- son objetos de JS
- ambos contienen información que influye en el resultado del _render_
- pueden tener valores por default
- pueden ser accedidos mediante `this.props` o `this.state`, pero estas propiedades son de _sólo lectura_. Tenemos que utilizar métodos como `setState` para modificarlos.

Entre las diferencias, encontramos

**Props:**

- se pasan a un componente, [siempre de arriba hacia abajo](https://github.com/undefinedschool/notes-react-principles#flujo-de-datos-unidireccional-one-way-data-flow).
- son _valores de configuración_. Podemos pensar en ellos como si se tratase de los argumentos que recibe una función.
- son _inmutables_, no podemos modificar el valor de una _prop_ desde el componente que la recibe.

**State:**

- se _administra_ dentro de un componente, similar a como funcionan las variables declaradas dentro de una función.
- un componente maneja su propio estado internamente, pero no modifica el estado de sus _child components_. Podríamos decir que el _state_ es _privado_ y el componente mismo se encarga de inicializarlo y modificarlo.
- siempre debe tener un valor inicial (default).
- es _mutable_, pero sólo puede modificarse por el componente que lo contiene (a través de `setState`).

**Es conveniente, en lo posible trabajar con componentes [_stateless_](https://github.com/undefinedschool/notes-react-basics#functional-o-stateless-components)s**, ya que manejar el _state_ agrega complejidad a nuestra aplicación.

> 👉 Ver más detalles en [_ReactJS: Props vs. State_](https://lucybain.com/blog/2016/react-state-vs-pros/).

### Debe un componente tener estado?

**El _state_ es totalmente opcional**. Dado que agregarlo agrega complejidad a la aplicación, es preferente utilizar, siempre que sea posible, [componentes sin estado](https://github.com/undefinedschool/notes-react-basics#functional-o-stateless-components).

> 👉 Si un componente necesita hacer uso de cierta información que puede cambiar entre _renders_, información que el componente mismo puede crear y modificar, vamos a utilizar [_componentes con estado_](https://github.com/undefinedschool/notes-react-basics#class-o-stateful-components).

**Algunos detalles a tener en cuenta:**

- JSX no es un _template_ sino una extensión de la sintaxis de JS.
- JSX existe de forma separada de React.
- `<foo-bar />` mientras que `<foo-bar>` no. **A diferencia de HTML, en JSX tenemos que cerrar los tags siempre**.

> 👉 Para más detalles, ver [_JSX in Depth_](https://reactjs.org/docs/jsx-in-depth.html).

## JSX

[JSX](https://facebook.github.io/jsx/) nos permite utilizar una sintaxis _similar a HTML_ en aplicaciones React, que pueda convivir con código JavaScript en un mismo archivo `.js`. [Babel](https://babeljs.io/) luego va a transformar (_transpilar_) este código y transformarlo en código JavaScript standard que el _engine_ (por ejemplo del browser) puede entender y ejecutar. Por lo tanto, _JSX nos permite escribir HTML dentro de JavaScript_.

Podemos escribir cualquier expresión válida en JS dentro de llaves `{}` y esta será evaluada.

Por ejemplo

```JSX
<a className='App-link' href={mdnLink} target='_blank' rel='noopener noreferrer'>
  Learn {jsFirst}
</a>
```

donde `mdnLink` y `jsFirst` son strings que recibimos como [_props_](https://github.com/undefinedschool/notes-react-basics#props) ó a través del [_state_](https://github.com/undefinedschool/notes-react-basics#state).

## Tipos de componentes

### Functional o _Stateless Components_

> 👉 **Sólo tienen props, (no _state_)**. Toda la lógica de este tipo de componentes depende de las _props_ que reciben, por lo tanto, son mucho más simples de entender (y testear).

En React, los _Stateless Components_ se definen utilizando funciones.

**Siempre van a renderizar el mismo output dado el mismo input**, es por esto que se los conoce como componentes _funcionales_ o _puros_, ya que vamos a definirlos utilizando [_funciones puras_](https://www.freecodecamp.org/news/what-is-a-pure-function-in-javascript-acb887375dfe/).

### Class o _Stateful Components_

> 👉 **Tienen _props_ y _state_.** También se los conoce a veces como _state managers_. Se encargan por ejemplo, de la comunicación cliente-servidor (HTTP requests), procesar datos y reaccionar a eventos del usuario. Toda esta lógica va a manejarse dentro de _Stateful Components_, mientras que lo relacionado a la visualización y formato de la misma debería delegarse a _Stateless Components_, para reducir la complejidad.

En React, los _Stateful Components_ se definen utilizando clases. Podemos escribir [clases](https://github.com/undefinedschool/notes-oop-js/blob/master/README.md#class) que _retornen HTML_.

**Usamos _Class Components_ si necesitamos acceder al [_state_](https://github.com/undefinedschool/notes-react-basics#state)**.

Primero necesitamos importar `Component`,

```js
import React, { Component } from 'react';
```

el cual vamos a extender para escribir nuestras propias clases.

```JSX
class App extends Component {
  render() {
    return (
      <div className='App'>
        <header className='App-header'>
          <img src={logo} className='App-logo' alt='logo' />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a className='App-link' href='https://reactjs.org' target='_blank' rel='noopener noreferrer'>
            Learn React
          </a>
        </header>
      </div>
    );
  }
}
```

#### Accediendo al _state_

Para acceder al [_state_](https://github.com/undefinedschool/notes-react-basics#state) desde una clase, llamamos a `[super](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/super)` desde el constructor. Recordemos que `App` extiende `Component`, por lo que al hacer esto, estamos llamando al constructor de `Component`.

Ahora tenemos acceso a la propiedad `state` y podemos modificar este objeto, setearle valores, etc.

```JSX
class App extends Component {
  constructor() {
    super();

    this.state = {
      jsFirst: 'JavaScript',
      mdnLink: 'https://developer.mozilla.org/en-US/docs/Web/JavaScript'
    };
  }
  render() {
    const { jsFirst, mdnLink } = this.state;

    return (
      <div className='App'>
        <header className='App-header'>
          <img src={logo} className='App-logo' alt='logo' />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a className='App-link' href={mdnLink} target='_blank' rel='noopener noreferrer'>
            Learn {jsFirst}
          </a>
        </header>
      </div>
    );
  }
}
```

#### Modificando el _state_

La forma que tenemos de modificar el [_state_](https://github.com/undefinedschool/notes-react-basics#state) en un [_Class Component_](https://github.com/undefinedschool/notes-react-basics/#class-o-stateful-components) es a través del método `setState` (que proviene de `Component`).

Volviendo al ejemplo anterior, si queremos, por ejemplo, modificar alguna propiedad del _state_ al hacer click en un botón, podríamos utilizar la propiedad `onClick`, que agrega un _listener_ (para un evento de tipo 'click') en el elemento `<button>` y recibe un [_callback_](https://github.com/undefinedschool/notes-callbacks) como parámetro. Este callback va a ejecutarse cada vez que se clickee el botón.

Combinando lo anterior entonces con el método `setState`<sup>2</sup>, podemos modificar el estado al clickear el botón. `setState` va a invocar luego a `render` (ya que modificamos el estado), para que el componente sea renderizado nuevamente y la UI refleje correctamente el cambio de estado.

En este caso, sólo estamos modificando la propiedad `jsFirst` del _state_ y dejando el resto igual que antes.

```JSX
return (
  <div className='App'>
    <header className='App-header'>
      <img src={logo} className='App-logo' alt='logo' />
      <p>
        Edit <code>src/App.js</code> and save to reload.
      </p>
      <a className='App-link' href={mdnLink} target='_blank' rel='noopener noreferrer'>
        Learn {jsFirst}
      </a>
      <button
        onClick={() =>
          this.setState({
            ...this.state,
            jsFirst: 'React'
          })
        }
      >
        Change text
      </button>
    </header>
  </div>
);
```

---

<sup>1</sup> Ver [_one-way data flow_](https://github.com/undefinedschool/notes-react-principles#flujo-de-datos-unidireccional-one-way-data-flow).

<sup>2</sup> Tener en cuenta que [`setState` es _asincrónico_](https://medium.com/@wereHamster/beware-react-setstate-is-asynchronous-ce87ef1a9cf3)
