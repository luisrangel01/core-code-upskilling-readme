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