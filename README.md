# ![React: Conceptos Básicos](https://i.imgur.com/O1pbl51.png)

### 👉 Ver [todas las notas](https://github.com/undefinedschool/notes)

## Contenido

- [React Component](https://github.com/undefinedschool/notes-react-basics#react-component)
  - [Props](https://github.com/undefinedschool/notes-react-basics#props)
  - [State](https://github.com/undefinedschool/notes-react-basics#state)
  - [Props vs State](https://github.com/undefinedschool/notes-react-basics#props-vs-state)
  - [Debe un componente tener estado?](https://github.com/undefinedschool/notes-react-basics#debe-un-componente-tener-estado)
- [JSX](https://github.com/undefinedschool/notes-react-basics#jsx)
  - [Fragments](https://github.com/undefinedschool/notes-react-basics#fragments)
  - [Comentarios](https://github.com/undefinedschool/notes-react-basics#comentarios)
- [Tipos de componentes](https://github.com/undefinedschool/notes-react-basics#tipos-de-componentes)
  - [Functional o Stateless Components](https://github.com/undefinedschool/notes-react-basics#functional-o-stateless-components)
  - [Class o Stateful Components](https://github.com/undefinedschool/notes-react-basics#class-o-stateful-components)
    - [Accediendo al _state_](https://github.com/undefinedschool/notes-react-basics#accediendo-al-state)
    - [Modificando el _state_](https://github.com/undefinedschool/notes-react-basics#modificando-el-state)
- [Estilos y CSS](https://github.com/undefinedschool/notes-react-basics#estilos-y-css)
  - [Global CSS](https://github.com/undefinedschool/notes-react-basics#global-css)
  - [Inline CSS](https://github.com/undefinedschool/notes-react-basics#inline-css)
  - [CSS-in-JS](https://github.com/undefinedschool/notes-react-basics#css-in-js)
  - [CSS Modules](https://github.com/undefinedschool/notes-react-basics#css-modules)
- [React Router](https://github.com/undefinedschool/notes-react-basics#react-router)
- [Context API](https://github.com/undefinedschool/notes-react-basics#context-api)
- [React Hooks](https://github.com/undefinedschool/notes-react-basics#react-hooks)
- [Higher Order Components](https://github.com/undefinedschool/notes-react-basics#higher-order-components)
- [Testing](https://github.com/undefinedschool/notes-react-basics#testing)
  - [PropTypes](https://github.com/undefinedschool/notes-react-basics#proptypes)
- [React Developer Tools](https://github.com/undefinedschool/notes-react-basics#react-developer-tools)
- [Create React App]()

---

## React Component

**Un componente es un bloque de código reutilizable e independiente**, una pieza de UI con contenido, estilos y comportamiento definidos.

En React, cada parte de la UI es un componente y cada componente tiene un [estado](https://github.com/undefinedschool/notes-react-basics#state).

Idealmente, [cada componente debería encargarse de una sola cosa](https://en.wikipedia.org/wiki/Single_responsibility_principle). Si crece demasiado, puede a su vez dividirse en _sub-componentes_. Es decir, aplicamos el mismo criterio que utilizamos a la hora de crear funciones u objetos en general.

> 👉 **La UI de nuestra aplicación va a terminar estando definida entonces como un [_árbol de componentes_](https://reactjs.org/docs/thinking-in-react.html#step-1-break-the-ui-into-a-component-hierarchy)**.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

### Props

Los [componentes](https://github.com/undefinedschool/notes-react-basics#react-component) reciben valores a través de diferentes parámetros a los que llamamos _props_ (por propiedades) y retornan el código necesario (usando [_JSX_](https://github.com/undefinedschool/notes-react-basics#jsx)) para renderizar los componentes. 

Podríamos decir que funcionan de forma similar a los _atributos HTML_, sólo que, en este caso, escribimos JSX en lugar de HTML y las _props_ pueden ser cualquier expresión válida en JS. Estos valores (_props_) podrán ser luego utilizados por el componente o pasados a un _child component_.

> 👉 **Las _props_ son inmutables y siempre se pasan de componentes superiores a componentes inferiores<sup id="cite_ref-1"><a href="#cite_note-1">[1]</a></sup>**, dicho de otra forma, desde un componente padre (_parent component_) hacia un componente hijo (_child component_).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

### State

Un [componente](https://github.com/undefinedschool/notes-react-basics#react-component) puede simplemente recibir [_props_](https://github.com/undefinedschool/notes-react-basics#props) y renderizarse. 

Por otro lado, **los componentes también pueden poseer un _state_, un objeto de JavaScript que se utiliza para almacenar información (características propias) acerca del componente y que puede cambiar a lo largo del tiempo**. Estos cambios suelen ser resultado de diferentes eventos producidos por los usuarios (input en un formulario, click sobre un elemento, etc) o el sistema (obtener el resultado de hacer un request a una API, etc).

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

**Si necesitamos compartir el _state_ de un componente con otros, lo pasamos por [_props_](https://github.com/undefinedschool/notes-react-basics#props), siempre de arriba hacia abajo, de un _parent_ a un _child component_**. En la práctica, esto implica que el componente raíz (_root_, el que se encuentra arriba de todo en el árbol de componentes) de la aplicación necesita tener acceso a este valor en su [_state_](https://github.com/undefinedschool/notes-react-basics#state).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

### Props vs State

Tanto las _props_ como el _state_ tienen características comunes:

- son objetos de JS.
- ambos contienen información que influye en el resultado del _render_.
- pueden tener valores por default.
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
- es _mutable_, pero sólo puede modificarse por el componente que lo contiene, utilizando `setState`.

**Es conveniente, en lo posible trabajar con componentes [_stateless_](https://github.com/undefinedschool/notes-react-basics#functional-o-stateless-components)**, ya que manejar el _state_ agrega complejidad a nuestra aplicación.

> 👉 Ver más detalles en [_ReactJS: Props vs. State_](https://lucybain.com/blog/2016/react-state-vs-pros/).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

### Debe un componente tener estado?

**El _state_ es totalmente opcional**. Dado que agregarlo agrega complejidad a la aplicación, es preferente utilizar, siempre que sea posible, [componentes sin estado](https://github.com/undefinedschool/notes-react-basics#functional-o-stateless-components).

> 👉 Si un componente necesita hacer uso de cierta información que puede cambiar entre _renders_, información que el componente mismo puede crear y modificar, vamos a utilizar [_componentes con estado_](https://github.com/undefinedschool/notes-react-basics#class-o-stateful-components).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

## JSX

[JSX](https://facebook.github.io/jsx/) nos permite utilizar una sintaxis _similar a HTML_ en aplicaciones React, que pueda convivir con código JavaScript en un mismo archivo `.js`. [Babel](https://babeljs.io/) luego va a transformar (_transpilar_) este código y transformarlo en código JavaScript standard que el _engine_ (por ejemplo del browser) puede entender y ejecutar. Por lo tanto, _JSX nos permite escribir HTML dentro de JavaScript_.

> 👉 **Podemos escribir cualquier expresión válida en JS dentro de llaves (`{}`) y esta será evaluada**.

Por ejemplo

```JSX
<a className='App-link' href={mdnLink} target='_blank' rel='noopener noreferrer'>
  Learn {jsFirst}
</a>
```

donde `mdnLink` y `jsFirst` son strings que recibimos como [_props_](https://github.com/undefinedschool/notes-react-basics#props) ó a través del [_state_](https://github.com/undefinedschool/notes-react-basics#state).

**Algunos detalles a tener en cuenta:**

- JSX no es un _template_ sino una extensión de la sintaxis de JS.
- JSX existe de forma separada de React.
- `<foo-bar />` mientras que `<foo-bar>` no. **A diferencia de HTML, en JSX tenemos que cerrar los tags siempre**.
- para los _atributos de clase_, usamos `className` en lugar de `class`, ya que `class` es una _keyword_ de JS que usamos para construir _clases_ (OOP).

> 👉 Para más detalles, ver [_JSX in Depth_](https://reactjs.org/docs/jsx-in-depth.html).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

### Fragments

Si necesitamos devolver múltiples elementos, sin agregar innecesariamente nodos extra al DOM (como un `div` que haga de _contenedor_), podemos utilizar [_React Fragments_](https://reactjs.org/docs/fragments.html) para agrupar y devolver una lista de nodos.

```JSX
render() {
  return (
    <React.Fragment>
      <ChildA />
      <ChildB />
      <ChildC />
    </React.Fragment>
  );
}
```

Alternativamente, podemos utilizar una sintaxis abreviada (`<></>`). Tener en cuenta que esta última no soporta _keys_ o atributos.

```JSX
render() {
  return (
    <>
      <ChildA />
      <ChildB />
      <ChildC />
    </>
  );
}
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

### Comentarios

No podemos utilizar comentarios de HTML directamente dentro de _JSX_, porque pueden interpretarse como nodos del DOM.

> ❌ esto no funciona!

```JSX
render() {
  return (
    <div>
      <!-- This doesn't work! -->
    </div>
  );
}
```

Si queremos utilizar comentarios entonces, debemos escribir comentarios de JS de la forma `/* */`, dentro de llaves `{ }` (**los comentarios con `//` no funcionan, sólo `/* */`**).

> ✅ esta es la forma correcta.

```JSX
render() {
  return (
    <div>
      { /* This works! */}
    </div>
  );
}
```

También podemos escribir comentarios multi-línea, de la forma

```JSX
render() {
  return (
    <div>
      {/* 
        Multi
        line
        comment
      */}
    </div>
  );
}
```

> 👉 **Notar que los comentarios deben siempre incluirse dentro de otro elemento. Si queremos escribirlos de forma separada, podemos utilizar [_Fragments_](https://github.com/undefinedschool/notes-react-basics#fragments)**.

Ejemplo con comentario suelto, utilizando _Fragments_.

```JSX
render() {
  return (
    <>
      {/* 
        hi
        there
      */}
      <p>Hello, React dev!</p>
    </>
  );
}
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

## Tipos de componentes

### Functional o _Stateless Components_

> 👉 **Sólo tienen props, (no _state_)**. Toda la lógica de este tipo de componentes depende de las _props_ que reciben, por lo tanto, son mucho más simples de entender (y testear).

En React, los _Stateless Components_ se definen utilizando funciones.

**Siempre van a renderizar el mismo output dado el mismo input**, es por esto que se los conoce como componentes _funcionales_ o _puros_, ya que vamos a definirlos utilizando [_funciones puras_](https://www.freecodecamp.org/news/what-is-a-pure-function-in-javascript-acb887375dfe/).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

#### Modificando el _state_

La forma que tenemos de modificar el [_state_](https://github.com/undefinedschool/notes-react-basics#state) en un [_Class Component_](https://github.com/undefinedschool/notes-react-basics/#class-o-stateful-components) es a través del método `setState` (que proviene de `Component`).

Volviendo al ejemplo anterior, si queremos, por ejemplo, modificar alguna propiedad del _state_ al hacer click en un botón, podríamos utilizar la propiedad `onClick`, que agrega un _listener_ (para un evento de tipo 'click') en el elemento `<button>` y recibe un [_callback_](https://github.com/undefinedschool/notes-callbacks) como parámetro. Este callback va a ejecutarse cada vez que se clickee el botón.

Combinando lo anterior entonces con el método `setState`<sup id="cite_ref-2"><a href="#cite_note-2">[2]</a></sup>, podemos modificar el estado al clickear el botón. `setState` va a invocar luego al método `render` (ya que modificamos el estado), para que el componente se vuelva a renderizar y la UI refleje el cambio de estado correctamente.

> 👉 **Es importante notar que sólo modificamos el _state_ a través de `setState`** y no hacemos, por ejemplo `this.state.jsFirst = ...`. `setState` modifica el estado y luego llama a `render`, para que los cambios se produzcan siempre de forma _unidireccional_.

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

## Estilos y CSS

Como vimos antes, usando la _prop_ `className`, podemos agregarle clases de CSS a un componente, donde el valor de `className` hará referencia a clases definidas en hojas de estilo CSS externas.

```JSX
render() {
  return <span className="menu navigation-menu">Menu</span>;
}
```

Generalmente, las clases dependen de las _props_ o el _state_ del componente

```JSX
render() {
  let className = 'menu';
  
  if (this.props.isActive) {
    className += ' menu-active';
  }
  
  return <span className={className}>Menu</span>;
}
```

> Este tipo de código puede simplificarse usando el paquete [`classnames`](https://www.npmjs.com/package/classnames#usage-with-reactjs)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

### Global CSS

Podemos agregar estilos con CSS a nuestro proyecto con simplemente linkear una hoja de estilos en el `index.html` que monta nuestros componentes, como lo haríamos con HTML y CSS normalmente y referirnos a las clases definidas en este CSS a través del atributo `className`.

```html
<link rel="stylesheet" href="styles.css" />
```

También podemos importar el `.css` en el `index.js`. En el caso de que estemos utilizando [CRA](https://github.com/facebook/create-react-app), Webpack se dará cuenta de que `'./index.css'` es un archivo CSS y va a aplicarlo al componente `App`, a través de un atributo `style`.

```JSX
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css'; // importing .css file
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

> 👉 El problema con aplicar estilos de esta forma, es que son **globales** (este es el comportamiento por default de CSS), por lo tanto no podríamos _scopear_ estilos a un componente determinado, sino que tendríamos un _namespace global_, complejizando así la reusabilidad de los estilos.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

### Inline CSS

Al igual que en HTML, React nos permite también aplicar estilos _inline_, utilizando el atributo `style`.<sup id="cite_ref-3"><a href="#cite_note-3">[3]</a></sup>

Los estilos inline se definen usando objetos de JS en lugar de strings, con propiedades escritas en la versión [_camelCase_](https://en.wikipedia.org/wiki/Camel_case) del nombre de la propiedad CSS. Podemos pasar los estilos directamente o crear un objeto que los contenga y pasarlo como _prop_.

Por ejemplo

```JSX
const divStyle = {
  color: 'blue',
  backgroundImage: 'url(' + imgUrl + ')',
};

function HelloWorldComponent() {
  return <div style={divStyle}>Hello World!</div>;
}
```

Los estilos inline también nos permiten combinar sintaxis de CSS con [_JSX_](https://github.com/undefinedschool/notes-react-basics#jsx).

En React, el atributo `style` se usa con mayor frecuencia para añadir estilos calculados dinámicamente al momento del renderizado.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

### CSS-in-JS

**_CSS-in-JS_ es un término que se utiliza para definir un _patrón_ donde el CSS se escribe usando JavaScript**, en lugar de definirlo en hojas de estilo externas. De esta forma, **podemos definir estilos dentro del _scope_ de un componente**,es decir, dejan de ser globales y pasan a ser locales, **modularizando de esta forma el CSS y haciéndolo reutilizable**.

Para más detalles, ver slides de la charla [React: CSS-in-JS - Christopher "vjeux" Chedeau](https://speakerdeck.com/vjeux/react-css-in-js) y esta [comparación de librerías CSS-in-JS](https://github.com/MicheleBertoli/css-in-js).

> 👉 **Esta funcionalidad no forma parte de React**, sino que es proporcionada por terceros. **React no es opinionado respecto de cómo se definen los estilos**.

[![The Road to Styled Components - Max Stoiber (React Conf 2017)](https://img.youtube.com/vi/jjN2yURa_uM/0.jpg)](https://www.youtube.com/watch?v=jjN2yURa_uM)
> Ver [The Road to Styled Components - Max Stoiber (React Conf 2017)](https://www.youtube.com/watch?v=jjN2yURa_uM)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

### CSS Modules

Un _módulo CSS_ es un archivo CSS donde todos los estilos tienen un _scope_ local por default.

En React, cada component tiene su propio archivo VSS, _scopeado_ a ese componente. Para aplicarle estilos a un componente, sólo tenemos que crear un `.css` que contenga los estilos.

Luego, este CSS es compilado, generando una versión modificada del CSS, con las clases renombradas (para evitar colisiones en el _namespace_) y un objeto JS que el componente recibirá como _prop_, con las clases originales mapeadas a las nuevas. 

![What are CSS Modules?](https://miro.medium.com/max/1786/1*X5zB3tI5_xaNe3QVS2lNjg.png)
> Ver [_What are CSS Modules? A visual introduction_](https://www.javascriptstuff.com/what-are-css-modules/)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

## React Router

[notas aparte]

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

## Context API

[notas aparte, conceptos avanzados]

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

## React Hooks

[notas aparte]

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

## Higher Order Components

[notas aparte, conceptos avanzados]

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

## Testing

[notas aparte, conceptos avanzados]

(WIP)

### PropTypes

Podemos utilizar [*PropTypes*](https://reactjs.org/docs/typechecking-with-proptypes.html) para verificar tipos de las props de cada componente y chequear que estén siendo utilizados con los valores correspondientes, asi como validar que esté recibiendo las props requeridas.

> 👉 Tener en cuenta que **los *PropTypes* sólo se chequean en *runtime* (tiempo de ejecución de la app) y en modo desarrollo**, por cuestiones de performance.

```js
import PropTypes from 'prop-types';

class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

Greeting.propTypes = {
  name: PropTypes.string
};
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

## React Developer Tools

Una extensión que nos va a facilitar mucho la vida a la hora de _debuggear_ y entender nuestras aplicaciones React, son las _Developer Tools_, que nos permiten inspeccionar los componentes como si de elementos HTML se tratase.

> 👉 Descargar [React Developer Tools para Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=es)

> 👉 Descargar [React Developer Tools para Firefox](https://addons.mozilla.org/es/firefox/addon/react-devtools/)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

## Create React App

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-react-basics#contenido)

---

<sup id="cite_note-1"><a href="#cite_ref-1">1</a></sup> Ver [_one-way data flow_](https://github.com/undefinedschool/notes-react-principles#flujo-de-datos-unidireccional-one-way-data-flow).

<sup id="cite_note-2"><a href="#cite_ref-2">2</a></sup> Tener en cuenta que [`setState` es _asincrónico_](https://medium.com/@wereHamster/beware-react-setstate-is-asynchronous-ce87ef1a9cf3).

<sup id="cite_note-3"><a href="#cite_ref-3">3</a></sup> Por cuestiones de [_especificidad_](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) y mantenimiento del código, se recomienda usar _clases_ antes que estilos _inline_.
