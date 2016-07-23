# React.js Fundamentals
Exercises and project of [React.js Fundamentals course](http://courses.reactjsprogram.com/courses/reactjsfundamentals)


## Notes from the course

Declarative vs Imperative code
React is kind of declarative (mostly in its componets). You can have the state in the react, not only the DOM.

Think in terms of components! *Composition*

### React is just javascript! But this course will teach some other things as well
- Learn map
- Learn bind
- Understand more 'this'
- React router
- Webpack - code bundler
- Babel - code transformation
- JSX
- Axios


### NPM
To start npm in the folder, $npm init.

To save a dependency in the package.json file, $npm install <module> --save

### Webpack
It is a code bundler.

What it needs to know:
  1. Your root JS file
  2. Which transformations to make in the code
  3. Location to spit the transformed code

The Webpack config file is called `webpack.config.js` and needs to be located in the root directory,

`// In webpack.config.js - example with a coffeeScript loader
module.exports = {
  entry: [
    './app/index.js'
  ],
  module: {
    loaders: [
      {test: /\.coffee$/, exclude: /node_modules/, loader: "coffee-loader"}
    ]
  },
  output: {
    filename: "index_bundle.js",
    path: __dirname + '/dist'
  },
}
`

To run webpack, first you have to install it. To install globally, `npm install -g webpack`. Then, to keep webpack watching your files and to run it whenever they change, `webpack -w`. To ship for production, `webpack -p`. This will do the previous and minify your code.

### Babel.js
* Transforms JSX (and ES2015/2016) into JS.

`npm install --save-dev babel-core babel-loader babel-preset-react`

To run Babel inside Webpack, first you have to make a `.babelrc` file:

`{
  "presets": [
    "react"
  ]
}`
