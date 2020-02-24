> El siguiente contenido fue elaborado por [@_nhsz](https://twitter.com/_nhsz) como guía para las clases de [undefined school](https://twitter.com/undefinedSchool)
> Son bienvenidos los _issues_ y _PRs_ para mejorar el contenido, corregir errores, etc. 

> 👉 Si te resultó útil, **se agradece que lo compartas para que le llegue a más gente!**

# React: Conceptos Básicos

## Notas sobre React

- [**React: Principios**](https://github.com/undefinedschool/notes-react-principles/)
- [**React: Conceptos Básicos**](https://github.com/undefinedschool/notes-react-basics)

## Contenido

---

## Function o _Stateless Components_

## Class o _Stateful Components_

Podemos escribir [clases](https://github.com/undefinedschool/notes-oop-js/blob/master/README.md#class) que _retornen HTML_.

Para eso, primero necesitamos importar `Component`

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
