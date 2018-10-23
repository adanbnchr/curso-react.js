# React



# ¿Por qué React?


## Popularidad

- [Lo demanda el mercado](https://www.hntrends.com/2018/jun-no-signs-of-slowing-for-react.html?compare1=React&compare2=AngularJS&compare3=Angular+2&compare4=Vue)

- Gran comunidad
  - Stackoverflow
  - Librerías de terceros


- Muchas empresas
    - Facebook, WhatsApp, Instagram
    - Uber
    - Khan Academy
    - Airbnb
    - Dropbox
    - Netflix
    - PayPal


## A nivel técnico

- Excelente rendimiento: Virtual DOM

- Componentes reusables
  - Y existen muchos componentes

- Curva de aprendizaje pequeña
  - Fácil escribir con JSX
  - No salimos del estándar ES2015 y más allá


## Concepto de react

- Se considera la V en un modelo MVC
- Cada vista está constituida por componentes
  - Header
  - Footer
  - LogInForm
  - ...
- Cada componente se puede reutilizar en:
  - Otra vista 
  - Otra aplicación


## Instalación de paquetes

- Trabajaremos con el ecosistema node:
  - Instalaremos node, npm a través de nvm
  - Se puede usar [yarn](www.yarnpkg.com) como gestor de paquetes en vez de npm


## Ventajas de yarn
- Instantánea de versiones mediante *yarn.lock*
- Instalar dependencias en paralelo
  - Mayor rapidez
- Se empezó a usar mucho en el ecosistema React
  - React viene de Facebook y yarn también
- Con npm v6 no se aprecian ventajas

```bash
npm i -g yarn
yarn --version
```



# Introducción React y JSX


## Scripts de React

- No usaremos webpack
- [CDN relacionado con los paquetes de npm](https://unpkg.com)

  ```js
  unpkg.com/:package@:version/:file
  ```

- [Utilizaremos CDN](https://reactjs.org/docs/cdn-links.html)

  ```html
  <script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
  ```


# Esqueleto

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Código inicial</title>
</head>

<body>
  <div id="app"></div>
  <script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
  <script src="/scripts/app.js"></script>
</body>

</html>
```


## Estructura html

- Cargamos los siguientes scripts:

  - React y React-dom

- Generarán dos variables en el objeto Window:

  - React y   ReactDOM

- El segundo script está asociado a la web
  - No es necesario si trabajamos con VR ([react-360](https://facebook.github.io/react-360/))
  - No es necesrio con móviles ([react native](https://facebook.github.io/react-native/))


## Linter
- Para usar eslint, utilizaremos node:

  ```js
  npm init
  npm i -D eslint
  npx eslint --init
  ```

- Yo elijo standard


## Babel

- Es un compilador de JavaScript
  - Escribimos código JavaScrit de última generación
  - Babel lo traduce a código ES5
- Prueba a escribir código [en su web](https://babeljs.io/) y observa su traducción


## Hola Mundo mediante js

```js
console.log('App running')

const p = document.createElement('p') // Creamos un elemento párrafo
const text = document.createTextNode('Hola Mundo') // Creamos un nodo de tipo texto
p.appendChild(text) // Añadimos el texto al párrafo>
const appRoot = document.getElementById('app')
appRoot.appendChild(p)
```


## ¿Qué tenemos?

- Inyección de código html a partir de creación y relación de nodos
- Puede haber muchos nodos y se puede volver complejo


## ¿Qué nos gustaría?

- Elegir un nodo (app)
- Inyectar directamente el código dentro del nodo como si fuera código *html*
- ¡JSX al rescate!


## Lenguaje JSX

- JSX denota una ampliación de JavaScript a JavaScript con XML
  - Facilita el uso de templates

```js
/* global ReactDOM */
console.log('Aplicación en ejecución')

var template = <p>¡Hola Mundo!</p>
var appRoot = document.getElementById('app')
ReactDOM.render(template, appRoot)
```


## Necesitamos Babel

- Si ejecutamos en un navegador vemos que la definición del template da error:

```js
  var template = <p>¡Hola Mundo!</p>
  Unexpected token <
```

- No es código JavaScript
- Es una extensión (JSX) que nosotros debemos compilar previamente a JS para que funcione
- De eso se encarga Babel con el preset adecuado (react)


## Usar Babel

- Traduce el código anterior mediante Babel y comprueba que funcione en el navegador:

```js
/* global ReactDOM */
console.log('Aplicación en ejecución')

var template = <p>¡Hola Mundo!</p>
var appRoot = document.getElementById('app')
ReactDOM.render(template, appRoot)
```


## Resultado Babel

- Este es el código que deberíamos poner en el fichero _app.js_:

```js
/* global React, ReactDOM */
'use strict'

console.log('Aplicación en ejecución')

var template = React.createElement('p', null, '\xA1Hola Mundo!')
var appRoot = document.getElementById('app')
ReactDOM.render(template, appRoot)
```


## Uso automático de Babel

- Objetivos:
  - Escribir JSX y que se traduzca a código JavaScript
  - Escribir ES2015 y posterior y que se traduzca a ES5
  - ¡Qué sea automático!


## Plugins de Babel

- Babel está compuesto por un conjunto de plugins
- Cada plugin se encarga de hacer una traducción determinada
- [Plugin de funciones flecha](https://www.npmjs.com/package/babel-plugin-transform-es2015-arrow-functions)
- Se puede volver un poco locura seleccionar los plugins necesarios para traducir nuestro código a ES5
  - Utilizaremos **presets**
    - Son colecciones de plugins agrupados de forma lógica


## Presets de Babel

- Conjunto de plugins que hacen que Babel nos de una funcionalidad determinada.
- Nos facilitan la selección de los plugins
- Utilizaremos
  - **react**: que da acceso a JSX
  - **env**: da acceso a ES2015, ES2016 y ES2017


## Organización del proyecto

- Creamos carpeta *public* para el proyecto final
  - Fichero *index.html* en la carpeta public
  - Solo modificaremos los js
- Creamos carpeta *public/scripts* para los js en ES5
- Nuestros fuentes en el directorio *src* 
  - Fichero *app.js*


## Dependencias

- babel para compilación a ES5
- [live-server](https://www.npmjs.com/package/live-server) para visualización

  ```bash
  npm i -D babel-cli
  npm i -D babel-preset-react babel-preset-env
  npm i -D live-server
  ```


## Configuración del workflow

- liveserver coge los cambios y los muestra de forma automática en el navegador
- babel observa los cambios y compila para que liveserver los muestre en tiempo real (--watch o -w)

- npm scripts en *package.json*:
  ```bash
    "build": "babel -w src/app.js --out-file public/scripts/app.js  --presets=env,react",
    "start": "live-server ./public",
    "start-dev": "npm run build & npm start
  ```


## Ejecución y parada del proyecto

- Mediante dos comandos:

  ```bash
    npm run build
    npm start
  ```

- De una sola vez:

  ```bash
  npm run start-dev
  ```


## Explorar JSX

- [Instalamos Babel JavaScript](https://marketplace.visualstudio.com/items?itemName=mgmcdermott.vscode-language-babel)
  - Mejora colores sintáxis

- Escribiremos el código con paréntesis y salto de línea para mejor lectura:

  ```jsx
  const template = (
    <div>
      <h1>Lista de tareas</h1>
      <p>Pendientes:</p>
      <ol>
        <li>Planchar</li>
        <li>Comprar leche</li>
      </ol>
    </div>
  )
  ```


## Uso de expresiones

```js
const user = {
  name: 'Pepe',
  age: 30,
  city: 'Zaragoza'
}
const template = (
  <div>
    <h1>{user.name}</h1>
    <p>Age: {user.age}</p>
    <p>City: {user.city}</p>
  </div>
)
```


## Uso de condicionales

```js
const user = {
  name: 'Pepe',
  age: 30,
  city: 'Zaragoza'
}
function getCity (city) {
  if (city) {
    return <p>Ciudad: {city}</p>
  }
}
const template = (
  <div>
    <h1>{user.name ? user.name : 'Desconocido'}</h1>
    {user.age && user.age >= 18 && <p>Edad: {user.age}</p>}
    {getCity(user.city)}
  </div>
)
```


## Crear un header

- Crea un template para header con las siguientes propiedades:
  - title: *Añadir cervezas*
  - subtitle: *Usa el formulario para añadir tus cervezas preferidas*
- Crea un template que muestre:
  - El título mediante etiqueta h1
  - El subtítulo en caso de existir, mediante etiqueta de párrafo


## Solución header

- ¡Ojo, en principio se necesita una etiqueta que haga de wrapper!

```js
/* global ReactDOM */

const header = {
  title: 'Añadir cervezas',
  subtitle: 'Usa el formulario para añadir tus cervezas preferidas'
}

const template = (
  <header>
    <h1>{header.title}</h1>
    {header.subtitle ? <p>{header.subtitle}</p> : ''}
  </header>
)

var appRoot = document.getElementById('app')
ReactDOM.render(template, appRoot)
```


## Var, const y let

- Redeclarar variables
  - Es posible con var (let y const no dejan)
  - La compilación de lo siguiente en babel dará error:

  ```js
  let nombre = 'pepe'
  let nombre = 'pepe'
  ```


## Ambito de scope

- var dentro de funciones
- let y const dentro de llaves
  - Por eso definimios firstName fuera del if

  ```js
  const fullName = 'Pedro Pérez'
  let firstName

  if (fullName) {
    firstName = fullName.split(' ')[0]
    console.log(firstName)
  }
  console.log(firstName)
  ```


## Funciones tradicionales

- Forma tradicional:

```js
function square(x) {
  return x * x;
}
console.log(square(3));
```


- La función podría ser anónima
  - En este caso la guardamos en una variable para poder usarla

```js
const square = function (x) {
  return x * x;
};
console.log(square(3));
```


## Arrow functions

- Son funciones anónimas
  - En caso de usarlas posteriormente, hay que asignarlas a una variable
- Los parámetros van entre parentesis
  - Si hay un solo parametro puede ir sin paréntesis
  - Si no hay parámetros hay que poner paréntesis sin argumentos

  ```js
  const square = x => {
    return x * x
  }
  console.log(square(3))
  ```


- Arrow functions simplificadas:
  - Se quitan las {} y el return va implícito
    ```js
    const square = (x) => x * x

    console.log(square(3))
    ```
  - Si se devuelve un json, se deben añadir paréntesis:
    ```js
    const square = (x) => ({doble: x * x})
    ```


## Conversión a arrow functions

- Crea una arrow function que devuelva la primera parte de un nombre completo

```js
getFirstName('Pedro Pérez') -> "Pedro"
// Create regular arrow function
// Create arrow function using shorthand syntax
```


## Solución arrow function

```js
const getFirstName = fullName => fullName.split(' ')[0]
console.log(getFirstName('Pedro Pérez'))
```


## arguments

- No se pude acceder al array de arguments desde las arrow functions:

```js
const add = (a, b) => {
  // console.log(arguments)
  return a + b
};
console.log(add(55, 1, 1001))
```


## this

- Se comporta algo diferente en JavaScript respecto a otros lenguajes
  - Su valor depende de como se ha llamado, del contexto de la función
- Usando arrow funcions siempre depende del elemento superior
- Conclusiones:
  - Normalmente se deben utilizar arrow funcions
  - Pero en ocasiones no


## Ejemplo uso this

- ¿Funcionará el siguiente código?
  - ¿Sabes arreglarlo en caso de que no funcione?

```js
const user = {
  name: 'Pepe',
  cities: ['Zaragoza', 'Madrid', 'Lérida'],
  showCities: function () {
    this.cities.forEach(function (city) {
      console.log(`${this.name} ha vivido en ${city}\n`)
    })
  }
}
```


## Resultado

- La variable this no tiene valor en el console.log

```js
app.js:11 Uncaught TypeError: Cannot read property 'name' of undefined
    at app.js:11
```


## Posible solución:

```js
const user = {
  name: 'Pepe',
  cities: ['Zaragoza', 'Madrid', 'Lérida'],
  showCities: function () {
    const that = this
    this.cities.forEach(function (city) {
      console.log(`${that.name} ha vivido en ${city}\n`)
    })
  }
}
```


## Solución con Arrow funcions

```js
const user = {
  name: 'Pepe',
  cities: ['Zaragoza', 'Madrid', 'Lérida'],
  showCities: function () {
    this.cities.forEach((city) => {
      console.log(`${this.name} ha vivido en ${city}\n`)
    })
  }
}
```


## ¿Funcionará?

```js
const user = {
  name: 'Pepe',
  cities: ['Zaragoza', 'Madrid', 'Lérida'],
  showCities: () => {
    this.cities.forEach(city => {
      console.log(`${this.name} ha vivido en ${city}\n`)
    })
  }
}
```


## Solución:
- No funciona porque la función flecha coge *this* de su *parent scope*
- En este caso su *parent scope* es el *global scope* :-(
- Afortunadamente tenemos una nueva sintáxis para los métodos en las clases de ES6:

```js
const user = {
  name: 'Pepe',
  cities: ['Zaragoza', 'Madrid', 'Lérida'],
  showCities () {
    this.cities.forEach(city => {
      console.log(`${this.name} ha vivido en ${city}\n`)
    })
  }
}
```


## Eventos y atributos

- Algunos se deben reescribir
  - class -> className (class es palabra reservada en JavaScript)
- Se escriben con notación camelCase
- [Elementos que podemos usar en React](https://reactjs.org/docs/dom-elements.html)


## Ejemplo

- Completa el código siguiente para que los botones funcionen:

```js
/* global ReactDOM */
console.log('Aplicación en ejecución')

let count = 0
const addOne = () => {
  console.log('addOne')
}

const template = (
  <div>
    <h1>Count: {count}</h1>
    <button onClick={addOne}>+1</button>
    <button onClick={minusOne}>-1</button>
    <button onClick={reset}>reset</button>
  </div>
)

const appRoot = document.getElementById('app')

ReactDOM.render(template, appRoot)
```


## Solución código anterior

```js
/* global ReactDOM */
console.log('Aplicación en ejecución')

let count = 0
const addOne = () => {
  count++
}
const minusOne = () => {
  count--
}
const reset = () => {
  console.log(count)
  count = 0
}
const template = (
  <div>
    <h1>Count: {count}</h1>
    <button onClick={addOne}>+1</button>
    <button onClick={minusOne}>-1</button>
    <button onClick={reset}>reset</button>
  </div>
)

const appRoot = document.getElementById('app')

ReactDOM.render(template, appRoot)
```


## Análisis código anterior

- Los botones funcionan
- Sin embargo no se renderiza de nuevo al cambiar el valor de *count*


## Implementación del render

- Tenemos que llamar al render de forma manual
  - Al inicio de la aplicación
  - Cada vez que se pulsa un botón
- ReactDOM.render es muy eficiente:
  - Solo actualizará la parte del DOM necesaria
  - Utiliza un DOM virtual para ver diferencias
  - Actulizará solo el h1, no los botones
- ¿Lo intentas?


## Solución

```js
/* global ReactDOM */
console.log('Aplicación en ejecución')

let count = 0
const addOne = () => {
  count++
  renderApp()
}
const minusOne = () => {
  count--
  renderApp()
}
const reset = () => {
  count = 0
  renderApp()
}

const appRoot = document.getElementById('app')

const renderApp = () => {
  const template = (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={addOne}>+1</button>
      <button onClick={minusOne}>-1</button>
      <button onClick={reset}>reset</button>
    </div>
  )

  ReactDOM.render(template, appRoot)
}

const appRoot = document.getElementById('app')
renderApp()
```


## Eventos

- [Lista de eventos](https://reactjs.org/docs/events.html)
- [Eventos del formulario](https://reactjs.org/docs/events.html#form-events)

```js
/* global ReactDOM */

const app = {
  title: 'Añadir cervezas',
  subtitle: 'Usa el formulario para añadir tus cervezas preferidas',
  cervezas: []
}

const onFormSubmit = e => {
  e.preventDefault()
  const cerveza = e.target.elements['cerveza'].value
  if (cerveza) {
    app.cervezas.push(cerveza)
    e.target.elements.cerveza.value = ''
    renderApp()
    console.log(app.cervezas)
  }
}

const renderApp = () => {
  const template = (
    <div>
      <header>
        <h1>{app.title}</h1>
        {app.subtitle ? <p>{app.subtitle}</p> : ''}
      </header>
      <form onSubmit={onFormSubmit}>
        <input type="text" name="cerveza" />
        <button>Añadir cerveza</button>
      </form>
    </div>
  )
  const appRoot = document.getElementById('app')
  ReactDOM.render(template, appRoot)
}

renderApp()

```


## Ejercicio: borrar lista

- Implementar un botón de borrado
- Implementar la acción del botón
  - Inicializar el array de cervezas a vacío.
  - Renderizar de nuevo

```js
const template = (
  ....
  <button onClick={onRemoveAll}>Remove All</button>
  ...
);

const onRemoveAll = () => {
  app.cervezas = []
  renderApp()
}
```


## Solución ejercicio

```js
/* global ReactDOM */

const app = {
  title: 'Añadir cervezas',
  subtitle: 'Usa el formulario para añadir tus cervezas preferidas',
  cervezas: []
}

const onFormSubmit = e => {
  e.preventDefault()
  const cerveza = e.target.elements['cerveza'].value
  if (cerveza) {
    app.cervezas.push(cerveza)
    e.target.elements.cerveza.value = ''
    renderApp()
  }
}

const onRemoveAll = e => {
  e.preventDefault()
  app.cervezas = []
  renderApp()
}

const renderApp = () => {
  console.log(app.cervezas)
  const template = (
    <div>
      <header>
        <h1>{app.title}</h1>
        {app.subtitle ? <p>{app.subtitle}</p> : ''}
      </header>
      <form onSubmit={onFormSubmit}>
        <input type="text" name="cerveza" />
        <button onClick={onRemoveAll}>Remove All</button>
        <button>Añadir cerveza</button>
      </form>
    </div>
  )
  const appRoot = document.getElementById('app')
  ReactDOM.render(template, appRoot)
}

renderApp()
```


## Uso de Arrays con JSX

- Basta con poner en el template algo como:

  ```js
  {
    ["cerveza1", "cerveza2", "cerveza3"]
  }
  ```

- JSX lo sabe pintar
- Aunque normalmente necesitaremos añadir marcas de párrafo:

```js
{
  [<p>cerveza1</p>, <p>cerveza2</p>, <p>cerveza3</p>]
}
```


- Observa el warning:
  _Each child in an array or iterator should have a unique key prop_...

  - NO tenemos comments de react
  - Añadimos el key que luego no se visualiza pero lo usa internamente para chequear los cambios del DOM

```js
<ol>
  {app.cervezas.map(cerveza => (
    <li key={cerveza}>{cerveza}</li>
  ))}
</ol>
```


## Ejercicio

- Añadimos más campos a las cervezas y gestionamos un array de objetos
- Para mostrarlas en la lista ponemos solo el nombre, pero creamos botones que permitan ver el resto
- Puedes utilizar las siguientes slides de ayuda
  - Como hacer visible un elemento
  - Como leer los datos de un formulario y convertirlos a un json


## Ayuda visibilidad formulario

```js
let visibility = false

const toggleVisibility = () => {
  visibility = !visibility
  render()
}

const render = () => {
  const template = (
    <div>
      <h1>Visibility Toggle</h1>
      <button onClick={toggleVisibility}>
        {visibility ? "Ocultar detalles" : "Ver detalles"}
      </button>
      {visibility && (
        <div>
          <p>Ahora puedes ver los detalles</p>
        </div>
      )}
    </div>
  )

  ReactDOM.render(template, document.getElementById("app"))
}

render()
```


## Ayuda: formulario a JSON

- Los datos se recogen en una colección (formulario)
  ```js
  const elementsForm = e.target
  ```
- Para obtener los datos en JSON:
  - Se convierte la colección a un array
  - Se ejecuta el método reduce del array y cada elemento del array se convierte a un campo del objeto final
  - Podemos utizar *Array.from* o *call* que hace una conversión de tipos implícita


```js
const formToJSON = elements =>
[].reduce.call(
  elements,
  (data, element) => {
    if (element.value) data[element.name] = element.value
    return data
  },
  {}
)

const formToJSON = elements => {
  const newElements = Array.from(elements)
  return newElements.reduce((data, element) => {
    if (element.value) data[element.name] = element.value
    return data
  }, {})
}
```



# Clases ES6 y React components


## Clases ES6

- Creamos la clase persona:
  - Campo nombre, por defecto anónimo
  - Método saludar: *¡Hola soy xxxx!*
- Instanciamos para comprobar


```js
class Persona {
  constructor (name = 'Anónimo') {
    this.name = name
  }
  saludar () {
    return `Hola, soy ${this.name}`
  }
}

const pepe = new Persona('Pepe')
console.log(pepe.saludar())

const desconocido = new Persona()
console.log(desconocido.saludar())
```


## Ejercicio clases

- Añadimos el campo *edad*, por defecto 0
- Añadimos el método *presentarse* donde diga nombre y edad


## Solución clase

```js
class Persona {
  constructor (nombre = 'Anónimo', edad = 0) {
    this.nombre = nombre
    this.edad = edad
  }
  saludar () {
    return `Hola, soy ${this.nombre}`
  }
  presentarse () {
    return `Me llamo ${this.nombre} y tengo ${this.edad} años`
  }
}

const pepe = new Persona('Pepe', 26)
console.log(pepe.saludar())

const desconocido = new Persona()
console.log(desconocido.presentarse())
```


## Subclases

- Creamos la clase Estudiante que tiene los siguientes atributos:
  - Nombre
  - Edad
  - Grado (Informática, Inglés...)


```js
class Estudiante extends Persona {
  constructor (nombre, edad, grado) {
    super(nombre, edad)
    this.grado = grado
  }
  tieneGrado () {
    return !!this.grado
  }
  presentarse () {
    let presentación = super.presentarse()

    if (this.tieneGrado()) {
      presentación += ` He estudiado la carrera de ${this.grado}.`
    }

    return presentación
  }
}
```


## Ejercicio subclases

- Crea la clase viajero según los requerimientos siguientes:
    - Atributos:
      - Nombre
      - Edad
      - Ciudad de origen
    - Métodos:
      - Saludar, donde diga la ciudad de donde procede.


## Solución: clase Viajero

```js
class Viajero extends Persona {
  constructor(nombre, edad, ciudadDeOrigen) {
    super(nombre, edad)
    this.ciudadDeOrigen = ciuddDeOrigen
  }
  saludar() {
    let saludo = super.saludar()

    if (this.ciudadDeOrigen) {
      saludo += ` Procedo de ${this.ciudadDeOrigen}.`
    }

    return saludo;
  }
}

const Pepe = new Viajero('Pepe García', 26, 'Madrid')
console.log(Pepe.saludar())
```


## Create-react-app

- Nos evita tener que configurar Webpack o Babel
- ¿Qué incluye?

  - Soporte a React, JSX, ES6, TypeScript y Flow .
  - Soporte a E6 y superior mediante Babel
  - Prefijos CSS automáticos
  - Test runner con soporte de informe de coverage
  - Servidor de desarrollo en vivo
  - Webpack configurado para empaquetar JS, CSS e imágenes para producción


## Crear una nueva aplicación

  ```
  npx create-react-app cervezas
  cd my-app
  npm start # ejecución
  npm test # tests
  npm run build # compilación  
  ```


## Configurar linter

- create-react-app ya viene "predefinida"
  - Opciones de Babel
  - Webpack
  - eslint
  - ....
- Podemos hacer *npm run eject* para ver lo que hay por debajo
  - ¡No hay vuelta atrás!
- Pero nos da la opción de configurar prettier


## Prettier

- Instalación:
  ```
  npm i -D prettier
  ```
- [Configuración (fichero prettierrc.json)](https://prettier.io/docs/en/configuration.html)
  - Por ejemplo:
    ```js
    {
    "tabWidth": 2,
    "semi": false,
    "singleQuote": true
    }
    ```
  - Observa autocompletado del editor para personalizar prettier


## Vistazo a la aplicación por defecto

- Se utilizan imports y exports de ES6
- Se importan CSS e imágenes gracias a Webpack
- Se da estilos a los elementos vía el atributo *className*
- Nuestros componentes extienden de React.Component
  - Utilizan el método render para representarlos en el navegador (vía JSX)
  - Heredan otros métodos que no aparecen aquí


## Compilación

```
npm run build
npm i -g serve
serve -s build
```


## Preparación interfaz

![](./cervezas.png)


## Componentes React

- Dividiremos nuestra interfaz en varios componentes
  ```jsx
    <CervezasView />
    <Header />
    <Sidebar />
    <Menu />
    <CervezasList />
    <CervezaSnippet />
    ....
  ```


## Extensiones para React

- Configuramos emmet para que funcione con jsx:
  
  ```json
    "emmet.includeLanguages": {"javascript": "javascriptreact" }
  ```

- Usaremos una extensión de Visual Code Editor para React
  - [React Standard Style code snippets](https://marketplace.visualstudio.com/items?itemName=TimonVS.ReactSnippetsStandard)


## Crear componente Header

- Con el disparador *rce* tenemos la plantilla para nuestro primer componente

  ```jsx
    import React, { Component } from 'react'
    import Header from './Header'

    class App extends Component {
      render() {
        return <Header />
      }
    }

    export default App
  ```


## Modificación app.js

- Modificamos *app.js* para que cargue el Header:

  ```js
    import React, { Component } from 'react'
    import Header from './Header'

    class App extends Component {
      render() {
        return <Header />
      }
    }

    export default App
  ```


## Header configurable

- El Header va a ser un componente reusable entre otros sitios de mi web
- Me interesa que el título se pueda cambiar
  - Se envía como una propiedad
  - React permite hacer un checking de las propiedades para el desarrollo
    - Ese código se elimina cuando se hace el build
    - Se deben disparar los snippets mediante *pts, ptn, ptsr...*


## Código Header configurable

```js
  import React, { Component } from 'react'
  import PropTypes from 'prop-types'

  export class Header extends Component {
    static propTypes = {
      title: PropTypes.string.isRequired
    }

    render() {
      return (
        <header>
          <h1>{this.props.title}</h1>
        </header>
      )
    }
  }

  export default Header
```


## Llamada al Header con propiedades

- Se utilizan atributos "custom" 
- Se sigue la sintáxis de html
  
  ```js
  import React, { Component } from 'react'
  import Header from './Header'

  class App extends Component {
    render() {
      return <Header title="Buscador de cervezas" />
    }
  }

  export default App
  ```


## Ejercicio completar Header

- Añade la propiedad *subtitle* que, **si existe**, se debe renderizar con un párrafo


## Solución Header

```js
import React, { Component } from 'react'
import Header from './Header'

class App extends Component {
  render() {
    return (
      <Header
        title="Buscador de cervezas"
        subtitle="Elije la cerveza que más te guste para ver sus características"
      />
    )
  }
}

export default App
```


## Aplicar estilos

- Creamos un fichero Header.css:

```css
header {
  display: flex;
  flex-direction: column;
  align-items: center;
}
```


- Importamos el css dentro de nuestro componente Header:

```jsx
import React, { Component } from 'react'
import PropTypes from 'prop-types'
import './Header.css'

export class Header extends Component {
  static propTypes = {
    title: PropTypes.string.isRequired,
    subtitle: PropTypes.string
  }

  render() {
    return (
      <header className="header">
        <h1>{this.props.title}</h1>
        {this.props.subtitle && <p>{this.props.subtitle}</p>}
      </header>
    )
  }
}

export default Header
```


## Ejercicio

- Crea el resto de componentes y estilos para lograr algo similar a la captura de la aplicación de *cervezas*
  - breadcrumbs no es necesario
    - Importaremos un componente que interaccione con el enrutador
  - Los datos se pueden importar del fichero cervezas.json

    ```bash
    wget https://raw.githubusercontent.com/juanda99/curso-node-js-proyecto-api/master/data/cervezas.json
    ```



# Stateless functional components



# Enrutado


# Configurar layout

- Podemos definir el main de nuestra apliación mediante el paso de una propiedad:

```js
const Layout = (props) => {
  return (
    <div>
      <Header />
      {this.props.template}
      <Footer />
  )
}

ReactDOM.render(<Layout content={template} />, document.getElementById('app'))
```


## props.children

- Normalmente se hace utilizando la propiedad *children* que viene por defecto

```js
const Layout = (props) => {
  return (
    <div>
      <Header />
      {this.props.children}
      <Footer />
  )
}

ReactDOM.render(
  <Layout>
    <div>
      <p>Esto sería el main</p>
    </div>
  </Layout>, 
  document.getElementById('app'))
```

## Contanedores y componentes

- Los contenedores son los que reciben los datos
  - Se encargan de recibir los datos
  - Renderizan componentes (sus hijos), pasándoles las props que necesiten
- Los componentes "son tontos":
  - Reciben unos datos
  - A partir de dichos datos su estado/representación es siempre el mismo.


## Anidar componentes

- El componente View / Page, anidará todos los componentes de la página
- Algunos se utilizarán en alguna otra vista (<Header />, <Menu />...) otros no.


## Métodos y eventos

- Al pulsar el botón se debe solicitar vía ajax al servidor los datos necesarios
- Probemos con un alert
- La función ajax se enviará como propiedad (componente más reutilizable) 
  - Podría ser una petición ajax
  - Un filtro sobre los datos que ya hay
  - ....

```class AddOption extends React.Component {
  handleAddOption(e) {
    e.preventDefault();

    const option = e.target.elements.option.value.trim();

    if (option) {
      alert(option);
    }
  }
  render() {
    return (
      <div>
        <form onSubmit={this.handleAddOption}>
          <input type="text" name="option" />
          <button>Add Option</button>
        </form>
      </div>
    );
  }
}
```

# Propiedades por defecto

```js
class Greeting extends React.Component {
  // ...
}

Greeting.defaultProps = {
  name: 'Mary'
}
```

## Estado inicial
- Usando ***this.state***:

```js
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: props.initialCount};
  }
  // ...
}
```

## Uso de bind

```js
class SayHello extends React.Component {
  constructor(props) {
    super(props);
    this.state = {message: 'Hello!'};
    // This line is important!
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    alert(this.state.message);
  }

  render() {
    // Because `this.handleClick` is bound, we can use it as an event handler.
    return (
      <button onClick={this.handleClick}>
        Say hello
      </button>
    );
  }
}
```

## Otra opción

- Experimental
```
class SayHello extends React.Component {
  constructor(props) {
    super(props);
    this.state = {message: 'Hello!'};
  }
  // WARNING: this syntax is experimental!
  // Using an arrow here binds the method:
  handleClick = () => {
    alert(this.state.message);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Say hello
      </button>
    );
  }
}
```


## Clases o funciones

- [Clases vs funciones](https://frontarm.com/articles/es6-classes-vs-function-components/)


## Stateless functional components

- Muchos componentes son sencillos y no tienen estado
  - Deberían ser la gran mayoría de nuestra aplicación
- Se pueden crear mediante clases o funciones

- Más sencillos de leer
- Más fáciles para hacer tests

```js
const User = (props) => {
  return (
    <div>
      <p>Nombre: {props.nombre}</p>
      <p>Edad: {props.edad}</p>
    </div>
  )
}

ReactDOM.render(<User nombre='Pepe' edad={20} />, document.getElementById('app'));
```

## Valores por defecto

User.defaultProps = {
  age: 0
}


## Debug

- Utilizaremos las [React Dev Tools](https://github.com/facebook/react-devtools)



# Webpack


## ¿Qué es webpack?

- Un empaquetador de módulos (module bundler)
  - Genera un achivo único con los módulos que necesita tu aplicación para funcionar.
  - Permite generar bundles independientes por cada página de tu app
    - Suelen ser aplicaciones con mucho JavaScript
    - Hace más rápida la carga
