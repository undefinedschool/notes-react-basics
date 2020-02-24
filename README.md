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

En React, cada parte de la UI es un componente y cada componente tiene un [estado]().

## State

El _state_ o estado de una aplicación, es un objeto de JavaScript que representa las características propias de un [componente]()

## Function o _Stateless Components_

## Class o _Stateful Components_

Podemos escribir [clases](https://github.com/undefinedschool/notes-oop-js/blob/master/README.md#class) que _retornen HTML_.

> 👉 Usamos _Class_ si necesitamos acceder al [state]() de la aplicación

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

```JSX
class App extends Component {
  constructor() {
    super();
    
    this.state = {};
  }

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
