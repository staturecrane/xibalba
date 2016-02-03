#XIBALBA

A tiny, ES2015-flavored templating library that allows for the quick and concentrated creation of small websites entirely through Javascript. I built it primarily as a learning exercise and challenge, but have found myself using it for all of my personal web projects and continue to add, remove and improve its features. At current, it's just over 80% tested.

#What Does It Do?

Nothing much different than any other templating library and certainly nothing better, but it does have a few features worth pointing out. 

#Compartmentalized Component Creation

Xibalba is meant to be extremely simple and concentrated, meaning that it takes very little to create a quick DOM element and render it on the screen. It encourages smart element encapsulation and dynamic updating.

```javascript 

import {Xibalba} from './xibalba.js';

const xi = new Xibalba; 

renderDiv();

function renderDiv(){
  //we simply use xi.create to return a Javascript object that is stored in div
  //xi.creat takes three arguments: the node element, optional text content, 
  //and an optional attributes object
  let div = 
    xi.create('div', void 0, {
      id: 'unique-id',
      onclick: someFunc,
      style: {
        width: window.innerWidth/2 + 'px'
      }
    });
  //a component is simply an array Xibalba objects 
  let component = [div];
  
  //container elements are completely emptied and reinitialized
  xi.setHTML(component, document.body);
  
}

```

#An integrated reactive store

Unlike React, wherein each component has a state which can be explicitly passed as props to other components, but remain local, each Xibalba instance can be initialized with a single store that components can subscribe to. By default, subscriptions can be used to register custom callbacks and to link component attributes to specific text content. 

Store utilizes es2015 maps to store and retrieve information, as well as register callbacks to update subscribed components. 

```javascript 
import {Xibalba, Store} from './xibalba.js';

const store = new Store();
const xi = new Xibalba(store);

//presuming we have pre-defined 'red' and 'blue' css classes
store.setStore('red', 'red');
store.setStore('newText', 'This text is red');

let component = [
  xi.create('h1', xi.subscribe('newText'), {
    class: xi.subscribe('red'),
    onclick: ()=>{
      store.setStore('red', 'blue')
      store.setStore('newText', 'This text is now blue')
    }
  })
];

xi.setHTML(component, document.body);

```
Now, when the h1 element is clicked, its subscribed attributes will automatically update, too. 


