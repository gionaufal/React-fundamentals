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

```// In webpack.config.js - example with a coffeeScript loader
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
```

To run webpack, first you have to install it. To install globally, `npm install -g webpack`. Then, to keep webpack watching your files and to run it whenever they change, `webpack -w`. To ship for production, `webpack -p`. This will do the previous and minify your code.

### Babel.js
* Transforms JSX (and ES2015/2016) into JS.

`npm install --save-dev babel-core babel-loader babel-preset-react`

To run Babel inside Webpack, first you have to make a `.babelrc` file:

```{
  "presets": [
    "react"
  ]
}```

----

###Props

props are to components what arguments are to functions.

example:
```var FriendsContainer = React.createClass({
  render: function(){
    var name = 'Tyler McGinnis'
    var friends = ['Ean Platter', 'Murphy Randall', 'Merrick Christensen']
    return (
      <div>
        <h3> Name: {name} </h3>
        <ShowList names={friends} />
      </div>
    )
  }
});

render: function(){
  var listItems = this.props.names.map(function(friend){
    return <li> {friend} </li>;
  });
  return (
    <div>
      <h3> Friends </h3>
      <ul>
        {listItems}
      </ul>
    </div>
  )
}
});

```

.map returns an array with the li elements.

### functions

f(D)=V

A function takes in some data and returns a view

```var getProfilePic = function (username) {
  return 'https://photo.fb.com/' + username
}
var getProfileLink = function (username) {
  return 'https://www.fb.com/' + username
}
var getProfileData = function (username) {
  return {
    pic: getProfilePic(username),
    link: getProfileLink(username)
  }
}
getProfileData('gionaufal')
```

To make these functions return some UI, all you have to do is use the render function in react.

```var ProfilePic = react.createClass({
    render: function(){
      return(
        <img src={'https://photo.fb.com/' + this.props.username} />
        )
    }
  })

  var ProfileLink = React.createClass({
     render: function() {
       return (
         <a href={'https://www.fb.com/' + this.props.username}>
           {this.props.username}
         </a>
       )
     }
   })

   var Avatar = React.createClass({
     render: function() {
       return (
         <div>
           <ProfilePic username={this.props.username} />
           <ProfileLink username={this.props.username} />
         </div>
       )
     }
   })
   <Avatar username="gionaufal" />
   ```

React 0.14 introduced Stateless Functional Components, so the code above can be written as below:

``` var ProfilePic = function (props) {
   return <img src={'https://photo.fb.com/' + props.username} />
 }
 var ProfileLink = function (props) {
   return (
     <a href={'https://www.fb.com/' + props.username}>
       {props.username}
     </a>
   )
 }
 var Avatar = function (props) {
   return (
     <div>
       <ProfilePic username={props.username} />
       <ProfileLink username={props.username} />
     </div>
   )
 }
 <Avatar username="tylermcginnis" />
 ```


React uses pure functions, there are no side effects. Given the same arguments, a function returns always the same result.

The benefits of this approach:
1. You don't need to know the current state of your app to run the function
1. It's easy to test
1. Easier to reuse

React components should be FIRST:
- Focused
- Independent
- Reusable
- Small
- Testable

----

###Stateless Functional components

Since is so common to react components to have only a render method, since React 0.14 you can remove the createClass abstraction and use just a plain function:

this code

```
var HelloWorld = React.createClass({
  render: function () {
    return (
      <div>Hello {this.props.name}</div>
    )
  }
})
ReactDOM.render(<HelloWorld name='Tyler' />, document.getElementById('app'))
```

can be written like this
```
function HelloWorld (props) {
  return (
    <div>Hello {props.name}</div>
  )
}
ReactDOM.render(<HelloWorld name='Tyler' />, document.getElementById('app'))
```
Besides being simpler to write, this way you can separate presentational components vs other components.
