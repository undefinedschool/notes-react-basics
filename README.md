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

## Props

Los [componentes](https://github.com/undefinedschool/notes-react-basics#react-component) reciben datos a través de diferentes parámetros a los que llamamos _props_ (por propiedades) y retornan el código necesario (usando [_JSX_](https://github.com/undefinedschool/notes-react-basics#jsx)) para renderizar los componentes. 

> 👉 **Las props son inmutables y siempre se pasan de componentes superiores a componentes inferiores<sup>1</sup>**, dicho de otra forma, desde un componente padre (_parent component_) hacia un componente hijo (_child component_).

## State

El _state_ o estado de una aplicación, es un objeto de JavaScript que representa las características propias de un [componente](https://github.com/undefinedschool/notes-react-basics#react-component)

## JSX

Podemos escribir cualquier expresión válida en JS dentro de llaves `{}` y esta será evaluada.

Por ejemplo

```JSX
<a className='App-link' href={mdnLink} target='_blank' rel='noopener noreferrer'>
  Learn {jsFirst}
</a>
```

donde `mdnLink` y `jsFirst` son strings que recibimos como [_props_](https://github.com/undefinedschool/notes-react-basics#props) ó a través del [_state_](https://github.com/undefinedschool/notes-react-basics#state)

## Function o _Stateless Components_

## Class o _Stateful Components_

Podemos escribir [clases](https://github.com/undefinedschool/notes-oop-js/blob/master/README.md#class) que _retornen HTML_.

> 👉 Usamos _Class_ si necesitamos acceder al [_state_](https://github.com/undefinedschool/notes-react-basics#state) de la aplicación

Primero necesitamos importar `Component`

```js
import React, { Component } from 'react';
```

el cual vamos a extender para escribir nuestras propias clases

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

### Accediendo al _state_

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

---

<sup>1</sup> Ver [_one-way data flow_](https://github.com/undefinedschool/notes-react-principles#flujo-de-datos-unidireccional-one-way-data-flow)
