# Week 2

## Palindrome strings

DESCRIPTION:

A palindrome is a word, phrase, number, or other sequence of characters which reads the same backward or forward. This includes capital letters, punctuation, and word dividers.

Implement a function that checks if something is a palindrome. If the input is a number, convert it to string first.

Examples(Input ==> Output)

``` bash
"anna"   ==> true
"walter" ==> false
12321    ==> true
123456   ==> false
```

Solutions:

``` javascript
function isPalindrome(line) {
  let result = true;
  const base = String(line);
  for (let index = 0;index < base.length/2;index++){
    if (base[index] !== base[(base.length - 1) - index]) {
      result = false;
      break;
    }
  }
  return result;
}
```

``` javascript
function isPalindrome(line) {
  const base = String(line);
  for (let index = 0; index < base.length / 2; index++) {
    if (base[index] !== base[base.length - 1 - index]) {
      return false;
    }
  }
  return true;
}
```

``` javascript
function isPalindrome(line) {
  return (String(line) == String(line).split('').reverse().join('')); 
}
```

## Well of Ideas - Easy Version

DESCRIPTION:

For every good kata idea there seem to be quite a few bad ones!

In this kata you need to check the provided array (x) for good ideas 'good' and bad ideas 'bad'. If there are one or two good ideas, return 'Publish!', if there are more than 2 return 'I smell a series!'. If there are no good ideas, as is often the case, return 'Fail!'.

Solutions:

``` javascript
function well(x){
  const count = x.filter((element) => element === 'good').length;
  return count > 2 ? 'I smell a series!' : count === 0 ? 'Fail!' : 'Publish!';
}
```


``` javascript
function well(x) {
  switch (x.filter(i => i === 'good').length) {
    case 0:
      return 'Fail!'
    case 1:
    case 2:
      return 'Publish!'
    default:
      return 'I smell a series!'
  }
}
```

## Managing Events in React JS

DESCRIPTION:

Write a react component that will display the current value of our counter.

The counter should start at 0.
There should be a button to add 1.
There should also be a button to subtract 1.
We want to be able to see the value of the counter - so it should be rendered! And for your buttons to work they will need an onClick prop.

In your render you should return:

The counter display element with an id of 'counter', containing the counter value.
An increment button with an id of 'increment'
A decrement button with an id of 'decrement'
Helpful docs on Events: https://reactjs.org/docs/handling-events.html

Solution:

``` jsx
import React from 'react';

export class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {counter: 0};
    
    this.add = this.add.bind(this);
    this.subtract = this.subtract.bind(this);
  }
  
  add() {
    this.setState(prevState => ({
      counter: prevState.counter + 1
    }));
  }
  
  subtract() {
    this.setState(prevState => ({
      counter: prevState.counter - 1
    }));
  }
  
  render() {
    return (
      <div>
        <h1 id='counter'>{this.state.counter}</h1>
          <button type="button" onClick={this.subtract} id='decrement'>
            Decrement
          </button>
          <button type="button" onClick={this.add} id='increment'>
            Increment
          </button>
      </div>
    )
  }
}
```

## Santa wish list form in ReactJS

DESCRIPTION:

Santa wants to simplify his life and offer children the possiblity to enter their wishlist via an online form.

The form should be a React component and should contain:

an input field for the child's name (with id 'name')
a text area to describe the wish (id: 'wish')
a drop-down indicating the priority of the wish, from 1 to 5 - default is 1 (id: 'priority')
the keys in the state to store the corresponding values should be named the same as the element's id
an onSubmit action calling the function handleSubmit
a function called handleSubmit, which
calls send (a function that is already provided as part of the injected properties props)
passes the current state as a parameter to send
calls event.preventDefault
it should be a controlled component (i.e. using onChange to bind input to the component's state)
Further reading:

React Forms: https://reactjs.org/docs/forms.html
Learn about Controlled Components: https://www.codewars.com/kata/control-the-beast-controlled-components-in-reactjs

Solutions:

``` jsx
const React = require("react");

class WishlistForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name:'',
      wish:'',
      priority:1
    }
    
    this.handleChange = this.handleChange.bind(this);
    this.handleInputChange = this.handleInputChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  
  handleChange(event) {
    this.setState({priority: event.target.value});
  }
  
  handleInputChange(event) {
    const target = event.target;
    const value = target.type === ' checkbox' ? target.checked : target.value;
    const name = target.name;
    
    this.setState({
      [name]:value
    })
  }
  
  handleSubmit(event) {
    this.props.send(this.state)
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
      <label>Nombre:
        <input id='name' type="text" value={this.state.name} onChange={this.handleInputChange} />
      </label>
  
      <label>Wish:
        <textarea id='wish' value={this.state.wish} onChange={this.handleInputChange} />
      </label>

      <label>
          Priority:
          <select id='priority' value={this.state.priority} onChange={this.handleChange}>
            <option value="1">1</option>
            <option value="2">2</option>
            <option value="3">3</option>
            <option value="4">4</option>
            <option value="5">5</option>
          </select>
        </label>
       
      </form>
    );
  }
};
```

``` jsx
const React = require("react")

class WishlistForm extends React.Component {
  constructor(props) {
    super(props)
    this.handleSubmit = this.handleSubmit.bind(this)
    this.state = {
      name: "",
      wish: "",
      priority: 1,
    }
  }

  handleSubmit(event) {
    event.preventDefault()
    this.props.send(this.state)
  }

  render() {
    const {name, wish, priority} = this.state
    return (
      <form onSubmit={this.handleSubmit}>
        <input id="name" value={name} onChange={e => this.setState({name: e.target.value})} />
        <textarea id="wish" value={wish} onChange={e => this.setState({wish: e.target.value})} />
        <select id="priority" value={priority} onChange={e => this.setState({priority: +e.target.value})}>
          <option value="1" />
          <option value="2" />
          <option value="3" />
          <option value="4" />
          <option value="5" />
        </select>
        <button />
      </form>
    )
  }
}
```

``` jsx
const React = require("react");

class WishlistForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name:'',
      wish:'',
      priority:1
    }
    
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  
  handleChange(event) {
    this.setState({priority: event.target.value});
  }
   
  handleSubmit(event) {
    this.props.send(this.state)
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
      <label>Nombre:
        <input id="name" value={this.state.name} onChange={e => this.setState({name: e.target.value})} />
      </label>
  
      <label>Wish:
        <textarea id="wish" value={this.state.wish} onChange={e => this.setState({wish: e.target.value})} />
      </label>

      <label>
          Priority:
          <select id='priority' value={this.state.priority} onChange={this.handleChange}>
            <option value="1">1</option>
            <option value="2">2</option>
            <option value="3">3</option>
            <option value="4">4</option>
            <option value="5">5</option>
          </select>
        </label>
       
      </form>
    );
  }
};
```

## Easter egg list in ReactJS

DESCRIPTION:

You decide to create a simple list of your favourite Easter eggs in React.

Challenge
Learn about nesting and listing React components.

The component EggList will set a prop called eggs which is an array of your favourite easter eggs e.g. "Lindt".
Loop through the props.eggs to output a unorder list of Easter eggs.
Each list item should be a component called EasterEgg with a prop name, to render the name in a li tag.
Each EasterEgg will need a key prop with a unique id. Use the index of the array for now.
About keys in React lists
While you can use the index of the array for a key because they should be unique among their siblings. However it is better to use unique values.

Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity

More on Lists and Keys

Solutions:

``` jsx
import React from 'react';

export const EggList = (props) => {
  const eggs = props.eggs;
  const listItems = eggs.map((element,index) =>
    <EasterEgg name={element} key={index} />
  );

  return (
    <ul>{listItems}</ul>
  );
};

export const EasterEgg = (props) => {
  return ( <li key={props.key}>{props.name}</li> );
};
```

``` jsx
import React from 'react';

export const EggList = ({eggs}) => {

  return (
    <ul>
    {eggs.map((item, key) => {
      return <EasterEgg key={key} name={item} />;
    })
    }
    </ul>
  );
  
};

export const EasterEgg = ({name}) => {
  return (
    <li>{name}</li>
  );
};
```

``` jsx
import React from 'react';


export const EggList = (props) => {
  return <ul>{props.eggs.map((egg, index) => <EasterEgg key={index} name={egg}/>)} </ul>
};

export const EasterEgg = (props) => {
  const name = props.name;
  return( <li key={name} >{name}</li>)

};
```

## PC upgrade specs using HOC in ReactJS

DESCRIPTION:

First steps to learning the basics of higher order components (HOC) in ReactJS

A HOC is a function that takes a component as the first parameter and returns a function wrapping the first parameter.

``` JSX
function withExample(Component) {
  return function(props) {
    return <Component />
  }
}
```

More about HOC: ReactJS docs.

If you complete this kata try Truncate paragraph using HOC in React JS.

Challenge
You're building a new feature on your e-commerce site which displays two computer specs - basic and pro.

The PcDisplay component is already built and expects 5 props. { title, price, cpu, ram, ssd }

You will need to build a withPriceModel HOC and using that to manage the price of the BasicModel and ProModel components.

Build a HOC called withPriceModel which takes the PcDisplay component for first param and price increase number for the second param.

withPriceModel will manage the price and must set a default price of 50.

BasicModel should use the default price set by withPriceModel

ProModel should use withPriceModel to increase the price by 60. Total price should be 110.

Since the withPriceModel is responsible for managing the price, ensure that it can't be overritten by passing in a price prop.

Solutions:

``` jsx
const React = require('react');

// Don't change PcDisplay
const PcDisplay = (props) => {
  return (<div>
  <h1>{props.title}</h1>
  <p id="price">£{props.price}</p>
  <ul>
    <li><label>CPU</label> <span>{props.cpu}</span></li>
    <li><label>RAM</label> <span>{props.ram}</span></li>
    <li><label>SSD</label> <span>{props.ssd}</span></li>
  </ul>
  </div>);
};

// Implement HOC -> returns a functions that wraps the passed in `PcDisplay` component
function withPriceModel(WrappedComponent, priceIncrease = 0) {
  return class extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        price: 50 + priceIncrease
      };
    }

    render() {
      return <WrappedComponent {...this.props} price={this.state.price}  />;
    }
  };
}


// Build basic and pro model components using `withPriceModel`
let BasicModel = withPriceModel(
  PcDisplay
);

let ProModel = withPriceModel(
  PcDisplay,
  60
);
```

``` jsx
const React = require('react');

const PcDisplay = (props) => {
  return (
    <div>
      <h1>{props.title}</h1>
      <p id="price">£{props.price}</p>
      <ul>
        <li><label>CPU</label> <span>{props.cpu}</span></li>
        <li><label>RAM</label> <span>{props.ram}</span></li>
        <li><label>SSD</label> <span>{props.ssd}</span></li>
      </ul>
    </div>
  );
};

const withPriceModel = (WrappedComponent, priceDiff = 0) => {
  const startPrice = 50;
  
  function WithPriceModel(props) {
    const { price, ...passThroughProps } = props;
    return <WrappedComponent price={startPrice + priceDiff} {...passThroughProps} />
  }
  
  return WithPriceModel;
};

const BasicModel = withPriceModel(PcDisplay);
const ProModel = withPriceModel(PcDisplay, 60);
```

``` jsx
const React = require('react');

// Don't change PcDisplay
const PcDisplay = (props) => {
  return (<div>
  <h1>{props.title}</h1>
  <p id="price">£{props.price}</p>
  <ul>
    <li><label>CPU</label> <span>{props.cpu}</span></li>
    <li><label>RAM</label> <span>{props.ram}</span></li>
    <li><label>SSD</label> <span>{props.ssd}</span></li>
  </ul>
  </div>);
};

// Implement HOC -> returns a functions that wraps the passed in `PcDisplay` component
let withPriceModel = (WrappedComponent, increment=0) => ({price,...rest}) =>  <WrappedComponent price={50+increment} {...rest}/>
  
// Build basic and pro model components using `withPriceModel`
let BasicModel =  withPriceModel(PcDisplay);

let ProModel = withPriceModel(PcDisplay, 60);
```