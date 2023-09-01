# About: React_guide
This repository covers almost all topics of React along with explanation and example. I have spent more than +100 hours to make this repo. If you find it helpful give it a star :)

# 01 What is React
React is a JS library for builing user interfaces. React is all about components, props and state management.
React really doesnt care whether it contains HTML or not. React dont know what browser is. React only cares about components and their states.
React hands over all its things to the ReactDOM which is a virtual DOM. It is responsible to communicate with the Real DOM and take all headach of what to show to the user.

If we make any changes in the component. React checks whether it make changes to the screen OR not. If yes, then it tells the reactDOM which then deal with Real DOM and so on. 

React determines how the component tree are currently looking and how they  should look like. Virtual DOM receives the difference (required changes) and then it manipulate the Real DOM accordingly.


It is **important** to note that whenever the state, context or props changes inside the component. React Re-evaluated/re-execute that component. Moreover, Re-evaluation doesn't mean Re-Rendering  the Real DOM. NO NOT at all.
Real DOM changes only when there is a difference between the tree of the previous state and current state. This makes React Fast.

**Example**
```bash
//previous state

<div>
<h1> Hello guys </h1>
</div>

//New state

<div>
<h1> Hello guys </h1>
<p>I am new guys</p>
</div>

```
React will compare both states and it will only insert the <p> tag in the Real DOM instead of Re-rendering the entire DOM. It will not touch the existing elements.
If you want to see this in action make a code in which on click a button a paragraph should be inserted. Then go to the elements in browser and note that on clicking button only the inserted paragraph will flash and rest of the HTML DOM wont be touched.

Also remember when ever a parent component is re-executed its child components will re-executed too.
So this means that If there is a component which have no need to re-execute will make our app slower. So this means by preventing such unnecessary re-executions and callbacks we can make our react app highly optimized. For such purpose we have React.memo hook

# 02 React Setup
just simple go to the terminal and go to your desired folder where you wanna create your app and type below commands:

```bash
npx create-react-app app_name 
```
(this will create a folder containg some default react conponents)
```bash
npm start
```

### How to update react app and its dependencies
```bash
"dependencies": {
    .....
    "react-scripts": "4.0.2",
    .....
  },
```

simple change the version to your desired version and re-run the following command:
```bash
npm install
```

# 03 React Basics

we write JS in imparative approach (step by step)
but in react we write code in declarative way
Always start your component function with Captipal letter

### Wrapper component in react
```bash
import "./Card.css";
function Card(props){
  const classes = 'card ' + props.className
  return (
    <div className={classes}>{props.children}</div>
  )
}
export default Card;
```

**NOTE:** here props.children will be the content which is inbetween <Card></Card>


### Setting state dependent on the previous state in react

The last - yet most important - step is to update the counter state in the best possible way. When updating some state based on its previous value, you should use pass a function to the state updating function (i.e., to setCounter(), in this example). This function automatically receives the previous value and should return the new value:
```bash
export default function App() {
    const [initialState, incrementedState]=React.useState(0);
    const incrementer = () => {
        incrementedState(prevState => prevState + 1)
```


2 way binding is used in form submission to reset the entered value once the form is submitted
```bash
add value={entredValue} in  you input tags 
```
```bash
and setEnteredValue('') in the onSubmitHandler
```


### Passing data from down to up (children to parent) in React
while passing data from up to down we use props
on the other hand while passing data from down to up we use pointers (pointer are also props but their name include on in the start)
ON connvention shows that the value of this prop is actually a function which will triggered when something will happing inside that component.
In short we will pass functions as value to the children elements and children will access them using props of components and those functions will contain data which we wanna pass to the parent element.

Summar: we create functions in parent elements then we pass these functions as values to the children element so that they could receive data from children element. since the function were originally created in the parent elements. The data will be pass to the parent element in this way.

Apni Zuban mai: Children Element parent element se puchta hai k tujhe data chahiye hai ya nahi? Parent kehta hai chahiye. Children kehta hai phir ek function bana aur mujhe pass ker mai us mai data daal ker tujhe bhejta hun as an argument Tu wahan se receive ker li.

### Types of components
1.Presentational, Stateless or dumb components: These are the components which do not manage any state they are just here for GUI
2.Smart or Stateful component: These components manages the state of the event
3. Controlled component: These components contains the main logic and control the other components

### Map function is used in rendering
map function transfroms and array or object into other kind of array or obj respectively by taking function as an argument.
map() takes a function that automatically receives the individual array item as an argument and returns the new value (to which the item should be transformed)
if you want to show or render some data from the array or list you must consider map function as it goes through each value and then apply a given function on it.


### For conditional rendering
you must use useState and SetState in terms of true and false after that assume a variable which should define the initial state of rendering after that use if else condition and assign a new value to the assumed variable and this conditional approach is called ternary expression

### && operator
```bash
syntax:
{condition && value }
```

on becoming the condition true the value will be satisfied

### Local Storage
Local storrage is a browsers built in storage used for storing data in the form of objects.
you can add objects as:
```bash
localStorage.setItem('isLoggedIn', '1')
```

and you can get data as:
```bash
localStorage.getItem('isLoggedIn')
```

# 04 Styling React Components
### Dynamic Inline Style

Inline styles always have highest priority
If you are entering style in the component tag then remember that style takes and object so add like this:
```bash
<label style={{color: !isValid ? 'red' : 'black'}}>Course Goal</label>

//here isValid is initial state -----> const [isValid, setIsValid] = useState(true);
```


But this will change this CSS permanently you have reset the state


### Adding classes Dynamically

We can add classes dynamically with the help of template literal

we have added some extra classes in CSS which will style our components as we want
```bash
// in CSS file

.form-control.invalid input {
  border-color: red;
  background-color: #ffd7d7;
}
.form-control.invalid label {
  color: red;
}

<div className={`form-control ${!isValid ? 'invalid' : ''}`}>
//in ${} we can also perform our JS expressions
```



### CSS modules

React app support CSS modules and all its transform to normal code to run in browser.
To use your CSS files as a module you have change its name like anyname.module.css

and instead of simply import it you have import it like:
```bash
import styles from './Button.module.css';
<button type={props.type} className={styles.button} onClick={props.onClick}> 
//button is a class having CSS properties in Button.module.css file
```
// now here "styles" will act as object and CSS classes will act as propteries for this (style) object.



**NOTE:** If you CSS property has name with dash then this syntax will not work you have to some different syntax like: 
```bash
<button type={props.type} className={styles['my-button']} onClick={props.onClick}> 
```

If you are adding classes dynamically on conditions then you can use this syntax of template literal:
```bash
<div className={`${styles['form-control']} ${!isValid ? styles.invalid: ''}`}>
```

**Note** that CSS modules and dyncamically adding classes work almost the same.

# 05 Debugging React App
As a programmer you will always face errors and your job is to resolve these errors.

Here are some tools you can use to debug your React code

For using chrome built-in  debugger go to sources-->elements-->localhost-->static/js-->C:/address...-->src

here you will find all your files simply go to the location where are facing errors and then add break point by  just simply clicking on it. Now perform some actions on your GUI and you can pause and execute your code step by step at the break points.

The second method is for chrome user

simple go to extensions and add "React Developer tool" exension in your browser and go to inspect and click on this >> icon and select components here you will see the tree strcutured of your React project which will make easier for you to analyze and debug your code

# 06 Fragments, Portals and Refs
There are JSX limitations for example as we know that we cannot return more than one root to function/component.We also cannot store more than one root JSX element in a variable.

**Solution 1:**
This problem has been solved by wrapping the whole code into a div container.

But this solution is not so efficient for bigger apps as there will so many unecessary deep div which are unnecessary but will render in the real DOM just because of this limitation. This approach is OK but not ideal

**Solution 2:**
You can make your own custom wrapper just like 
```bash
function wrapper(props){
	return props.children; // HERE props.children returns all the content around which it is wrapped
}
```
and then in other files you can use it as 
```bash
<wrapper>Your content (HTML, JSX etc.) </wrapper>
```
wrapper is nothing just an empty component. You may thing what the benefit of it. The advantage is that now this wrapper component will not render in the real DOM.


### React Fragments

instead of making wrappers you can simply use react fragments like
```bash
<React.Fragments>Your content (HTML, JSX etc.) </React.Fragments>
```

These fragments wont render in the real DOM

### Portals


Its not good to style a div like a button by adding eventlisteners into it and by adding the CSS styles this may would work but it not a good idea to style a div element as button.
Portals let you render children in some different part of DOM

**EXP1**

```bash
import { createPortal } from 'react-dom';
// ...

<div>
  <p>This child is placed in the parent div.</p>
  {createPortal(
    <p>This child is placed in the document body.</p>,
    document.body
  )}
</div>
```


**EXP 2:**
```bash
function SidebarContent() {
  return <p>This part is also rendered by React!</p>;
}

export default function App() {
  return (
    <>
      {createPortal(
        <SidebarContent />,
        sidebarContentEl
      )}
    </>
  );
}
```


### Refs (Hook)


Refs allow us to access DOM element and work with them. When you want a component to remember some info but not render it. Its basically a hook.
once you have made a connection between you rendering HTML element and your ref. You can console.log the value of ref you will get an object having current props.
if you want to get value then you can do something like that:
```bash
console.log(yourRefName.current.value) //yourValue
```

so we can say we can use this hook to read the values and remember it by saving it into some variable

React Hook "useRef" cannot be called at the top level. React Hooks must be called in a React function component

**EXP**
```bash
import React, { useRef, useState } from "react";
import Button from "../../UI/Button/Button";
import styles from "./CourseInput.module.css";

const CourseInput = (props) => {
  const [enteredValue, setEnteredValue] = useState("");
  const [isValid, setIsValid] = useState(true);
  const myInput = useRef();
  console.log(myInput.current.value)

  const goalInputChangeHandler = (event) => {
    if (event.target.value.trim().length > 0) {
      setIsValid(true);
    }
    setEnteredValue(event.target.value);
  };

  const formSubmitHandler = (event) => {
    setEnteredValue("");
    event.preventDefault();
    if (enteredValue.trim().length === 0) {
      setIsValid(false);
      return;
    }
    props.onAddGoal(enteredValue);
  };

  return (
    <form onSubmit={formSubmitHandler}>
      <div
        className={`${styles["form-control"]} ${
          !isValid ? styles.invalid : ""
        }`}
      >
        <label>Course Goal</label>
        <input
          value={enteredValue}
          type="text"
          onChange={goalInputChangeHandler}
          ref={myInput}
        />
      </div>

      <Button type="submit">Add Goal</Button>
    </form>
  );
};

export default CourseInput;

```

### Controlled Vs uncontrolled
Here above elements using ref are called uncontrolled components as by using ref we are accessing value by interacting with DOM but we are not controlling the state.

# 07 Advance Handling side effects
All the below hooks are used for dealing with the complex states.
 
### useEffect()


useEffect is a React Hook that lets you synchronize a component with an external system.
The main job of this hook is to handle the side effects. so for that you have underdstand what are side effects. Side effects are the action which are perform in the action of some entered data. For example form validation, http requests etc.
Its another hook use to manage side effects. it take two arguments one is callback function which  must be executed after every component evaluation if the specified dependencies are changed. These dependencies (full of arrays) are the second argument that we take.
```bash
useEffect = (()=>{}, [dependencies]);
```

Application Example: Once you created your app having login page once the user has entered all his detailed and once his profile has authenticated then if he reloads his page then the page should NOT ask him again to enter the credentials. So this means that we have somewhere persist this information so on reloading or coming back to the login page the user should not have any need to again enter his details.

UseEffect function runs once after all the components has ran.

### What to add what to NOT in dependencies


You learned, that you should add "everything" you use in the effect function as a dependency - i.e. all state variables and functions you used in there.

That is correct, but there are a few exceptions you should be aware:
Note we always select and add those thing in dependencies which may change in future. But those thing about which we are 100% sure that thing is not gonna change you dont need to enter that thing.
such as set state function which we get as a return from useState hook.

Also NO need to add built-in functions such as fetch(), localStorage etc. 
Also NO need to add variables or functions which you may have defined outside of you component

So long story short: You must add all "things" you use in your effect function if those "things" could change because your component (or some parent component) re-rendered. That's why variables or state defined in component functions, props or functions defined in component functions have to be added as dependencies!

Here's a made-up dummy example to further clarify the above-mentioned scenarios:
```bash
import { useEffect, useState } from 'react';
 
let myTimer;
 
const MyComponent = (props) => {
  const [timerIsActive, setTimerIsActive] = useState(false);
 
  const { timerDuration } = props; // using destructuring to pull out specific props values
 
  useEffect(() => {
    if (!timerIsActive) {
      setTimerIsActive(true);
      myTimer = setTimeout(() => {
        setTimerIsActive(false);
      }, timerDuration);
    }
  }, [timerIsActive, timerDuration]);
};
```

### Passing objects to dependencies
```bash
const { someProperty } = someObject; // destructuring
useEffect(() => {
  // code that only uses someProperty ...
}, [someProperty]);
```
This is a very common pattern and approach.

### useReducer()
Sometimes it becomes harder and error prone using useState due to the complexity of the state. In such scenarios this hook can be used as the replacement for useState().
```bash
function reducer(state, action) {
}
const [state, dispatch] = useReducer(reducer, initialArg, init?)
```

here init? is optional
here the state is same as useState that is you can say initial state. The second dispatch function is state updating function but will work differently from useState.
here initialArg will be in the form of object {key:value} instead of actual value as in the useState hook. Important point to note that the dipatch will call to reducer function for us.
here every time we call dispatch it will pass to action keyword in reducer function and action will be perform and an object
you can see state like this:
```bash
state = {key:value}
```

since dispatch is a setState function you can also specify its type and by using if else or switch case condition you can also merge other functionality into reducer function.
and this "type" keyword would be an array for action so we can see actions like that:
action: ['cool', 'hot']


**Example**
Managing state with useState hook:
```bash
import React, { useState } from "react";

const App = () => {
  const [count, setCount] = useState(0);
  function increment() {
    setCount((prevCount) => prevCount + 1);
  }
  function decrement() {
    setCount((prevCount) => prevCount - 1);
  }
  return (
    <div>
      <button onClick={decrement}>-</button>
      <span>{count}</span>
      <button onClick={increment}>+</button>
    </div>
  );
};

export default App;

```

**Converting State with useReducer:**
```bash
import React, { useReducer } from "react";

const App = () => {
  const ACTIONS = {
    INCREMENT: 'increment',
    DECREMENT: 'decrement'
  }
  function reducer(state, action) {
    if (action.type === ACTIONS.INCREMENT) {
      return { count: state.count + 1 };
    } else if (action.type === ACTIONS.DECREMENT) {
      return { count: state.count - 1 };
    } else {
      return state;
    }
  }
  const [state, dispatch] = useReducer(reducer, { count: 0 });
  function increment() {
    dispatch({ type: ACTIONS.INCREMENT });
  }
  function decrement() {
    dispatch({ type: ACTIONS.DECREMENT });
  }

  return (
    <div>
      <button onClick={decrement}>-</button>
      <span style={{ color: "white" }}>{state.count}</span>
      <button onClick={increment}>+</button>
    </div>
  );
};
export default App;
```

**NOTE** that dispatch(action) dispatch function take action as arguments.
so we can see our actions as:
- action= { type: ACTIONS.INCREMENT }
- action= { type: ACTIONS.DECREMENT }

### Optional Payload property

There is also a property other than "type" which we used to pass to reducer action for passing the information as we know info is not status which we send via type to reducer action.


### useState vs useReducer

- useState() is your main state management tool

- useReducer will be used when data is related to each other. This would be helpful for managing more complex state.

- You can first go with useState and then make it to reducer hook

### React useContext Hook
This hook allows us to pass and update data deeply in the tree (our app components tree).
This is very helpful like if you want to send some props to a component which is in another component then you dont need to go through complex way
**Method 1**
You simply have to createContext() This function will contain you data in the form of object which you want to pass. Simply wrap the parent component with thir wrapper:
```bash
```
```bash
// In app.js
import React, { createContext } from 'react';
export const myContext = React.createContext();
export default function App() {
return (
<myContext.provider value={{fruit: 'Apple' }}>
	<anyComponent/>
</myContext.provider>
)
}

// Here any component inside the wrapper of <myContext.provider> will have access to anything (we can pass any thing function, variable, obj) inside the value variable
```

now all the content in this wrapper have access to  variables in "value" you can provide as many varibales in the "value" you want even you can pass functions via values
now to consume it you have to go the file where you want to consume this data:


**Consuming the value of myContext**

now to consume context we use a hook called useContext;
```bash
import { useContext, myContext } from 'react';

function myComponent() {
  const fruitObject = useContext(myContext);
return (
<>
{fruitObject}
</>
)
```

**NOTE:** You can also pass functions in value keyword in your context component
Use context hook when you have to perform a very specific value or action

#### Best Practices to follow while using useContext
You can with the above code but its a good practice to follow some standards so goes like:
1. Create a separate file like a store which contains all your logic, states or variable which you want to use globally.
2. Instead of using <myContext.provider value={anyThing}> in App.jsx make a wrapper with any name in your store file which you have created.
3. Instead of direct import useContext hook in every file where you want to consume it. Create a custom hook and import that.

Now following all above rules step by step

#### Best Practices:
```bash
// contextStore.js
import React, { createContext, useContext } from 'react';

const myContext= React.creatContext();
export function useMyCustomHook(){
return useContext(myContext)
}

export function myProvider({children}) {
return (
<myContext.Provider value={{fruit:apple}}>
    {children}
</myContext.Provider>
)
}
```
Now all our values and logic is in Context store. Now instead of wrapping directing wrapping our components we will use our custom wrapper which is "myProvider" in this case. 
Instead of using useContext direct we will use our custom hook which is 
```bash
// in app.js
import {useMyCustomHook, myProvider} from 'react';
import 'myComponent' from './filePath';

export default function app(){
<myProvider>
    <myComponent/>
</myProvider>
}
//
```

```bash
//In myComponent.js where we want to use values from store.
import {useMyCustomHook} from 'react';

export default function myComponent(){
const myFruitObj = useMyCustomHook();
return (
<>
  {myFruitObj}
</>

)
}

```
### Limitations of React Context
It is not suitable for high optimized changes.
It should not be replace across all the components

### forwardRef()
```bash
const MyInput = forwardRef(function MyInput(props, ref) {
  return (
    <label>
      {props.label}
      <input ref={ref} />
    </label>
  );
});
```

forward ref is used to forward ref through multiple components.
and to work with imperativeHandle 

### useImperativeHandle Hooks

This Hook is use to make your ref work entirely different. OR you can say by this hook you can make your custom ref.
This Hook combined with forwardref will help you pass you ref value to multiple components to connect them by ref where connecting components by props doesnt make sense
```bash
useImperativeHandle(ref, callback, dependencies)
```  
OR
```bash
useImperativeHandle(ref, () => {}, [])
```

To use ImperativeHandle hook you must have to create some refs in you parent and child components between which you wanna make some relation.

Ok so let say I want to pass my ref functions (we know ref could be an obj or function which will work customly due to useImperativeHandle) to parent component.
so first create your ref using useRef and pass its value to the element like input tag etc.

now use useImperativeHandle and in second argument create you ref function. Now you can use these functions outside your child component WOOWWWW...!
so now go to your parent component or where you want to use them.
create another ref using useRef in parent component. 
and then you the element where you want link this ref. Create a callback function there you can use it like this: 
```bash
() => myParentRef.current.childRefFunction()
```
//Here childRefFunction is a ref function created in child component inside the useImperative Hook.
// and myParentRef is name of useRef like:  const myParentRef = useRef();



**Example:**
```bash
// Child Component
import {useImperativeHandle, useRef } from 'react';
function MyChild(ref) {
const closeRef = useRef();  
const confirmRef = useRef();  

useImperativeHandle(ref, () =>  {
return {
  focusCloseRef : () => closeRef.current.focus(),
  focusConfirmRef : () => confirmRef.current.focus()
}
}, [])
  return (
    <>
    <button ref={closeRef}>Close</button>
    <button ref={confirmRef}>Confirm</button>
    </>

  )
}
export default MyChild;

// Parent file
import { useRef } from 'react';
function App(ref) {
const appRef = useRef();  

return (
  <>
  <button onClick={()=> appRef.current.focusCloseRef}>Focus Close</button>
  <button onClick={()=> appRef.current.focusConfirmRef}>Focus Confirm</button>
  </>

)
}


export default App;

```

**NOTE:** You should not often use useImperativeeHandle there are very few specific cases of for its use.


# 08 Https request with React

Browser side app do not directly talk to the databases. Unless its a highly insecrue app. Cause By doing this you will loose your cedentials as important point to remember is that all files
including your JS can be access by the user. 
For talking to databases you always use backend. Such as Node.js PHP etc. You need to do routing React app will communicate with the backend via API

**EXTRA INFO:** If in your app you are using local storage for authentication then dont simply use it. use it with 'bycrypt' of 'secure local storage package' so that if the data is visible on
local storage then it must be visible in the form of hash code instead of actual value.
For talking to databases you always use backend. Such as Node.js PHP etc. You need to do routing React app will communicate with the backend via API

Here API is a very broad term simply means set of rules are clearly defined for an interface.
When we talk about http requests REST and GraphQL are some standards of API.


**axios API**: are used for dealing with responses and sending http requests, this api makes this dealing very simple. You can use it with any library.
There is another built in API called fetch API this is also used for dealing with responses

### fetch API

  //by default the method is GET

Dont forget fetch() is an asynchronous function. Means the result wont be there instantly it would be there somewhere in future.
fetch returns a promise so we have to handle that promise
Here response is a JSON obj not JS obj so we have to convert it too. you can do it by using json method on response obj. json() method also return a response we have to handle that too.
by using .then method again OR using await

you always have to do some following steps
 ```bash
 async function fetchMoviesHandler() {
    const response = await fetch("https://swapi.dev/api/films/");
    const data = await response.json();
    const transformedMovies = data.results.map((movieData) => {
      return {
        id: movieData.episode_id,
        title: movieData.title,
        openingText: movieData.opening_crawl,
        releaseDate: movieData.release_date,
      };
    });
    console.log(transformedMovies)
```

###Statuses
- 200 
- 404 etc.
Whenever you get any status back in the action of sending http request this means the request was successful.
If the status is other than OK then this means that the request was successful but there was an error.

### handling errors

always remember when we use .then() then we use .catch() to handle errors but in case of 
async await we use "try and except"


### Cleaning functions

we can use 
```bash
return console.log( ) 
```
to stops the exeution of the function once the task is completed

### Sending data POST method
fetch  method is use for both sending and receiving data
This is how you send data to the backend API.
React do not talk directly to the database but with backend API
```bash
async function addMovieHandler(movie) {
    const response = await fetch(
      "https://react-db9-default-rtdb.firebaseio.com/movies.json",
      {
        method: "POST",
        body: JSON.stringify(movie),
        headers: {
          "Content-Type": "application/json",
        },
      }
    );
    const data = await response.json();
    console.log(data);
  }

```


### JSON.stringify(anyArray/Obj)
This take method takes JS array and converts it into JSON object.

# 09 Custom Hooks

Custom hooks are functions that contains stateful logic.
With the help of custom hooks we can outsource stateful logic into re-usable functions.

Its simple to create a react hook. Simply create it like you create components and then call in the file where you wanna use it.

If you hook contains a state then everytime calling hook in other file will create separate state. It will not share the state.

React custom hook also returns an array of hook like useState hook
You can return what you want to return in your custom hooks. It could be anything, an array, an obj, a number etc.

**For example:**
```bash
// custom react hook file

import React from 'react';

const useCustomHook => (skinColor) {

>all logic

	return [name, age];
}

//In file where I want to use custom Hook

import React from 'react';

const App => () {

	const [name, age] = useCustomHook(Blue)
return 
 > your code

}

```

here name and age is the array which our custom hook returns and blue is argument which our custom hook take.
custom hooks can take any thing like arrays, obj and functions and custom hooks can also return any thing like arrays, obj, and functions etc.

#### Mature Example of custom hook
```bash
// File where we are creating out custom hook
import React, {useState} from 'react';

function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    return getStoredValue(key, initialValue);
// Here getStoredValue simply get the values from local storage if exists otherwise it returns the initial value.
  });
  useEffect(() => {
    secureLocalStorage.setItem(key, value);
  }, [value]);

  return [value, setValue];
}

export default useLocalStorage;


// File where we are using our custom hook
import {useLocalStorage} from './folder'
const [value, setValue] = useLocalStorage('myKey', 'myInitialValue') 
```


### JSON.stringify();
The JSON.stringify() static method converts a JavaScript value to a JSON string

### Infinite loop in custom hook
When we use custom hook which contains states and then if we use useEffect hook inside that custom hook then an infinite loop willl be generated. As the variables in the dependencies array will 
re-evaluated again again. And we know that in JS functions are objects and when ever the function is called even the same function is called again and again its a brand new object in memory.

to prevent this situation we have to wrap our customhook function in useCallback hook.



### Bind() method

This method can be apply to any function which is used to pre-configure the function. it takes two arugments 1st argument is the this keyword in the function on which we are applying this method and second method I will let you know after reading the documentation

# 10 Form in React
Most of the web is all about forms getting the data from the user and giving feedback accordingly. handling form can be a complex task when it comes to best user experience.
This include checking form validation whether the input is valid of not etc.


### Issues to deal and their solution
When ever a form is submit by clicking on press button the browser will automatically send the http request to the browser this will reload the page automatically and will restart the react application and we will loose our state. To prevent this always use
event.preventDefault() in submitHandler function

### Preventing Submitting empty form
To prevent submit empty form you must stops the execution of form submission handler function. You can do this by initializing states as true and false. check
if the input is false its stops the execution then appear an error otherwise go with the flow.
```bash
if enteredName === '' {
setState(false)}
```

**NOTE:** while setting states as true and false always set the initial state false because initially the form is empty and emtpy form is an invalid state
To give user a feedback about invalid input you can use old school CSS class.
first make a class of invalid input in css and then update the class conditionally and dynamically.
ALso make a state namely [touchedInput, setTouchedInput] for such purpose.

### Adding custom hook

Since the input form validation procedure will remain same for all other inputs so its a good idea to make a custom hook and call it in every components where it is needed. 
but make sure that your hook remain generic

There is link below which contains the code of a custom hook which is capabale of form validation. This hook will do all for us we just have to integrate this.

link: https://github.com/academind/react-complete-guide-code/tree/16-working-with-forms/code/12-finished/src

# 11 Redux
```bash
> npm install redux react-redux
```
If you want a centralized place to handle all of your states and any requests that will change that state. This is where Redux comes in. Redux is a state management library that allows us to create a store that holds all of our state. We can then dispatch actions to change that state.
Prop drilling: it occurs when a parent component passes data down to its children and then those children pass the same data down to their own children. At the end, it's a long chain of component dependencies that can be difficult to manage and maintain.

Redux consist of a reducer function that takes in the current state and an action and returns the new state. We can have multiple reducers that handle different parts of our state. 
**For example:** we could have a reducer that handles the user state and another reducer that handles the product state.
A **store** is a place to hold all of our state. We can then dispatch actions to change that state. We can also subscribe to the store to get the current state.
Redux is a JS library for statem management. Its also called flux like state propagation library

There are three type of states
1. local state (State that belongs to a single component which usually managed by useState() and useReducer() )
2. cross-component state (State that affect multiple component which require props chain and prop drilling)
3. app-wide state (State that affects the entire app)

Here useContext really solve the problem of passing data across the cross-component and app-wide component

### Redux vs. React Context
Why redux despite we have React context hook which also avoids the props drilling/props chaining?

Important point to note that we can use both redux and react context in same application.

If there is a situation is which a single component is taking multiple states from the other component then by using the react Context you will end with deeep context provider and context
consumer components which is not goood.

For such cases React Context will give you a complex setup to manage such states.
So inshort react context use is good for low frequency updates which are not suddenly updating, cause React context is not made for high performance.

Redux do not come up with such low frequency and complex setup with deep nested component problems


### How Redux works?

You will always have one store (Central Data/State Store)
Your all states would be in this single store. 
We can use this data inside our component. 
To change data in the store we will use Reducer Function (Its general concept in which perfrom some action on a set of data and generate a new output it is NOT that reducer funciton in the useReducer hook)
But who will trigger this reducer function?
The answer is actions.....as we know components run dispatch functions which are actions/or describe what should be done which will trigger the reducer function and then that reducer function will mutate the central data store and then it will send the updated value to components and so on.

Centeral store--->components---->Dipatch function--->action--->reducer function  (repeat)


### Reducer Function

This function takes two parameters 
- old state
- dispatched action 


**Output:** This reducer fucntion can return any thing but in most of the cases it will return new state object.

### This is how a basic redux look like in node js
```bash
const redux = require('redux');

const counterReducer = (state, action) =>{
    return  {
        counter: state.counter + 1
    }

}

const store = redux.createStore(counterReducer);

```


### This is how basic redux looks like in react
```bash
import { createStore } from "redux";
const initialState = {counter: 0,  showCounter: true}
const counterReducer = (state = initialState, action) => {
  if (action.type === "increment") {
    return {
      counter: state.counter + 1,
      showCounter:state.showCounter
    };
  }
  if (action.type === "decrement") {
    return {
      counter: state.counter - 1,
      showCounter:state.showCounter
    };
  }
  if (action.type === "increaseBy5") {
    return {
      counter: state.counter + action.amount,
      showCounter:state.showCounter
    };
  }
  if (action.type === "decreaseBy5") {
    return {
      counter: state.counter - action.amount,
      showCounter:state.showCounter
    };
  }
  if (action.type === "toggle") {
    return {
      showCounter:!state.showCounter,
      counter:state.counter
    };
  }
  return state;
};
const store = createStore(counterReducer);

export default store;
```

In this code simply a store is taking a reducer function namely counterReducer and our counterReducer function contains actions and dispatch i.e increment and decrement

now to use it go to the major index.js and in root component import provider and your store and wrap the app component inside the provider. This will make the child component of the app component to use the redux or you can say access the data in store :

```bash
// In index.js file:

import React from 'react';
import ReactDOM from 'react-dom/client';

import './index.css';
import App from './App';
import { Provider } from 'react-redux';
import store from './store/index';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Provider store={store}><App /></Provider>);
```

Now every child element of app have access to the redux store.

```bash
// File where we are using redux
import { useSelector, useDispatch } from "react-redux";
import classes from "./Counter.module.css";

const Counter = () => {
  const toggleCounterHandler = () => {
    dispatch({ type: "toggle" });
  };
  const dispatch = useDispatch();

  const counter = useSelector((state) => state.counter); //useSelector is getting data from state obj which is in store
  const show = useSelector((state) => state.showCounter); //useSelector is getting data from state obj which is in store

  const incrementHandler = () => {
    dispatch({ type: "increment" });
  };
  const decreaseHandler = () => {
    dispatch({ type: "decreaseBy5", amount:5 });
  };
  const increaseHandler = () => {
    dispatch({ type: "increaseBy5", amount: 5 });
  };
  const decrementHandler = () => {
    dispatch({ type: "decrement" });
  };
  
  return (
    <main className={classes.counter}>
      <h1>Redux Counter</h1>
      {show && <div className={classes.value}>{counter}</div>}
      <div>
        <button onClick={incrementHandler}>Increment</button>
        <button onClick={increaseHandler}>Increase by 5</button>
        <button onClick={decreaseHandler}>Decrease by 5</button>
        <button onClick={decrementHandler}>Decrement</button>
      </div>
      <button onClick={toggleCounterHandler}>Toggle Counter</button>
    </main>
  );
};

export default Counter;
```




### useSelector() Hook
This is a custom hook made by redux team. This hook allows us to get some part of data from redux store and will executed automatically by redux.

Now to dispatch actions we will use useDispatch() hook its also a redux hook 

### Pay load
```bash
const decrementHandler = () => {
    dispatch({ type: "decrement" , amount:5 });
  };
```

From dispatch function we are passing data to action object where amount is a payload. Payload is nothing just another key value pair sending to action


### Correct usage of state

you should NEVR EVER mutate the state.
for exp: state.counter++ this will mutate the state

Actually redux itself do not mutate the state it over write the current existing state.
So instead of mutating the state always return a brand new over writing state.

# 12 Redux Toolkit
>npm install @reduxjs/toolkit

### Redux Toolkit

while working with react there is a possibility where you can make a typo mistake while dispatching the actions.

Its not compulsory to use Redux tool kit but if you using this will make things little bit easier for you.

### Below is the basic redux toolkit sample
```bash
// In index.js (where we create our redux toolkit)

import { createSlice, configureStore } from "@reduxjs/toolkit";
const initialState = { counter: 0, showCounter: true };

const counterSlice = createSlice({
  name: "counter",
  initialState: initialState,
  reducers: {
    increment(state){
      state.counter++;
    },
    decrement(state){
      state.counter--;
    },
    increase(state, action){
      state.counter = state.counter + action.payload
    },
    decrease(state, action){
      state.counter = state.counter - action.payload
    },
    toggleCounter(state){
      state.showCounter = !state.showCounter
    }
  }

});

const store =configureStore({
  reducer: counterSlice.reducer   //here we are using reducer instead of reducers cause it will map each object automatically
})

export const counterActions = counterSlice.actions
export default store;
```


### Explanation
Here we will use createSlice instead of createStore. The createSlice take 3 arguments one is the name which you can set anything and other is the initail state and third is the reducers object which will contain our functions/actions which we want to perform.

The name of the functions you can create anything cause redux will automatically creates //{type: "UNIQUE_IDENTIFIER", payload: anyValue} and matches automatically. These functions take two arguments one is state and other is action for payloads.

here we are using state.counter++; WHYYY??? in normal redux we strictly avoided this mutation of state. DONT WORRY here it is not the case. Redux toolkit will automatically replace this mutation with over writing. 

here store is configured by using configueStore which takes an object. with key reducer and value of counterSlice.reducer. Here reducer 

then we are exporting the actions (our functions) so that we could use them in other files.


```bash
//In Counter file where we are using it
import { useSelector, useDispatch } from "react-redux";
import { counterActions } from "../store/index";
import classes from "./Counter.module.css";

const Counter = () => {
  const dispatch = useDispatch();
  const counter = useSelector((state) => state.counter); //useSelector is getting data from state obj which is in store
  const show = useSelector((state) => state.showCounter); //useSelector is getting data from state obj which is in store

  const toggleCounterHandler = () => {
    dispatch(counterActions.toggleCounter());
  };

  const incrementHandler = () => {
    dispatch(counterActions.increment());
  };
  const decreaseHandler = () => {
    dispatch(counterActions.decrease(5));
  };
  const increaseHandler = () => {
    dispatch(counterActions.increase(5)); //{type: "UNIQUE_IDENTIFIER", payload: 10}
  };
  const decrementHandler = () => {
    dispatch(counterActions.decrement());
  };

  return (
    <main className={classes.counter}>
      <h1>Redux Counter</h1>
      {show && <div className={classes.value}>{counter}</div>}
      <div>
        <button onClick={incrementHandler}>Increment</button>
        <button onClick={increaseHandler}>Increase by 5</button>
        <button onClick={decreaseHandler}>Decrease by 5</button>
        <button onClick={decrementHandler}>Decrement</button>
      </div>
      <button onClick={toggleCounterHandler}>Toggle Counter</button>
    </main>
  );
};

export default Counter;

```

### Exlanation

As usual we will use dispatch and useSelector to perform actions and get data respectively.
Now we will import counterAction object which contains our functions.

now we will use these functions in our event handler functions as methods on objects

for functions which require payloads simply pass the values payload to the functions as arguments.

### Important Point
here we should think about that when should we use redux. This will you know by experience. There is no need to always use redux. 


### Advance Redux

Your Redux function must be pure, side effects free, and synchronous function.

### Redux with async code. 

Since the reducer function must be side effects free. So while using http request or using async code where should we place this code then? Cause they may casue side effect to the reducer function. Such code must NOT goes into reducer function

WE have two choices
1. Either put such code in component.
2. Or put such code in selector generators.


So the best way is to keep your side effect logic in component using useEffect and data transformation login inside the reducer function when working with redux.

You must take into account that that useEffect will run for the first time when the file is executed for the first time. So in order to prevent this you must have to use useState by using true and false technique where you will run  execute your function when the condition is true.


### Thunk function

Thunk is function which delays an action until later.
It is an action creator function that does not return the action itself but another function which eventually returns the action

# 13 React Router DOM

To create React routers you only have to focus on three main files
- App.js
- Root.js
- MainNavigation.js

### File structure
```bash
npm install react-icons
```

### In src folder:
- index.js
- App.js
- App.css
- components (folder)
- assets (folder)

### In components folder:
- Component.jsx
- component.css
- all three sample file code is given below:

We must have anm idea what routing is. 
Here the path you enter in the web brower after the slash is basically a route or simply an address which you make an http request and server serves you with the respective files. 
You change the address and server send you files of different pages which should display to the user. This make the whole routing procedure slow and bad user experience as different HTML files are loading. 

Here comes the single page application where you only load the html files once and then JS takes the responsibility of should be shown to the client.


### Package
```bash
npm install react-router-dom
```
routes are nothing just mapping components 

### Defining Routes

This is how you define routes in React using createBrowserRouter for creating the route and RouterProvider to connect the route with the component
```bash
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import HomePage from "./pages/Home";
import ProductsPage from "./pages/Products";

const router = createBrowserRouter([
  { path: "/", element: <HomePage /> },
  { path: "/products", element: <ProductsPage /> },
]);
function App() {
  return (
    <>
      <RouterProvider router={router} />;
    </>
  );
}

export default App;
```

### Navigating between pages with links

There are two ways of doing this one is using simply a href in <a></a> tag this will do your work but the problem is by it this way will always send a new http req to the server and then the server will serve the respective page but in this way we are loading a whole JS and html page again. This is a lot of unnecessary work which will affect our performance.

To do this in right way we are now gonna use a module called link from react-router-dom

now instead of using <a></a> tag and href attribute we are gonna use <link> tag and "to" attribute instead of href
```bash
import {Link} from 'react-router-dom';
<Link to="/about">This is my About Page</Link>
```

by this is such way will prevent the brower to reload and will just render the desired component instead of loading the whole html and JS file again.


But what if when you will have several pages as we know nav bar will remain same in all pages so instead of adding nav bar component in all pages make a wraper root layout which will contain your nav bar you can do it by using Outlet module from react-router-dom

make a Root.js component file:
```bash
//root.jsx
import React from "react";
import MainNavigation from '../components/MainNavigation'
import { Outlet } from "react-router-dom";

function RootLayout() {
  return (
    <>
      <MainNavigation/>
      <Outlet/>
    </>
  );
}
export default RootLayout;
```

```bash
//MainNavigation component file:


import React from 'react'
import { Link } from 'react-router-dom';

function MainNavigation() {
  return (
    <nav>
        <ul>
            <li><Link to="/">Home</Link></li>
            <li><Link to="/products">Products</Link></li>
        </ul>
    </nav>
  )
}


export default MainNavigation;
    
```

```bash
//In App.js you have make parent and children relation as below:

import { createBrowserRouter, RouterProvider } from "react-router-dom";
import HomePage from "./pages/Home";
import ProductsPage from "./pages/Products";
import RootLayout from "./pages/Root";

const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    children: [
      { path: "/", element: <HomePage /> },
      { path: "/products", element: <ProductsPage /> },
    ],
  },
]);
function App() {
  return (
    <>
      <RouterProvider router={router} />
    </>
  );
}

export default App;
```


### Showing Error page on wrong URL
all thing will remain same. ofcourse you have to make an error component.
simply you just have to make some changes in app.js file as below:
```bash
//In App.jsx
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import HomePage from "./pages/Home";
import ProductsPage from "./pages/Products";
import RootLayout from "./pages/Root";
import ErrorPage from "./pages/Error";

//defining the routes
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    errorElement: <ErrorPage />,
    children: [
      { path: "/", element: <HomePage /> },
      { path: "/products", element: <ProductsPage /> },
    ],
  },
]);
function App() {
  return (
    <>
      <RouterProvider router={router} />
    </>
  );
}

export default App;
```

// here we simply used a builtin feature of react-router-dom that is errorElement and simply we have pointed toward our errorPage component which we want to show on occuring an error.

### Highlighting the active page on nav bar
In order to highlight the page which is currently showing you can use tag called NavLink you have to import it from react-router-dom
This link uses functions in className attribute and returns the name of class which we want to apply:
```bash
// In Main Navigation File:
import React from 'react'
import { NavLink } from 'react-router-dom';
import classes from './MainNavigation.module.css'

function MainNavigation() {
  return (
    <header className={classes.header}>
    <nav>
        <ul className={classes.list}>
            <li><NavLink to="/" className={({isActive})=> isActive ? classes.active : undefined }>Home</NavLink></li>
            <li><NavLink to="/products"className={({isActive})=> isActive ? classes.active : undefined }>Products</NavLink></li>
        </ul>
    </nav>
    </header>
  )
}


export default MainNavigation;
```
```bash
// In MainNavigation.module.css file

.list a:hover,
.list a.active {
    color: var(--color-primary-800);
    text-decoration: underline;
  }
```

### useNavigate() hook
This hook is used to programmatically hit the url
```bash
// In App.jsx
import {useNaviagte} from 'react-router-dom';

const navigate = useNavigate();

const function navigateButtonHandler() {
	naviate('/product')
}


export default function app() {
	return (
<button onClick="navigateButtonHandler">Navigator</Button>
	)
}

//on click this button you will go to the product page
```





### Defining and using Dynamic Routes

For defining routes dynamically you can use another hook called useParams

you can use this by importing it

agian you have to make some changes in app file:
```bash
{ path: "/products/:productId", element: <ProductDetails /> }
```

you have to give path in this syntax in chldren array.
here :productId this identifier is same as a variable. 
```bash
//Now in ProductDetails.js file
import React from "react";
import { useParams } from "react-router-dom";

function ProductDetails() {
  const params = useParams();

  return (
    <>
      <h1>Product Details</h1>
      <p>{params.productId}</p>
    </>
  );
}

export default ProductDetails;

```

Here params.productId will return the path which we will enter in the url after /products/




### Using Map function to display the list of products

If there are several products instead of writing them line by line and adding Link tag to it you can use map function to map over an array which contains all you info about your page and then iterate over it.
```bash
	<ul>
        {PRODUCTS.map((prod) => {
          return (
            <li key={prod.id}>
              <Link to={`/products/${prod.id}`}>{prod.title}</Link>
            </li>
          );
        })}
      </ul>
```


### Absoute vs Relative path

**The below is absolute path:**
```bash
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    errorElement: <ErrorPage />,
    children: [
      { path: "/", element: <HomePage /> },
      { path: "/products", element: <ProductsPage /> },
      { path: "/products/:productId", element: <ProductDetails /> }
    ],
  },
]);

```

**The below is relative path:**

```bash
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    errorElement: <ErrorPage />,
    children: [
      { path: "", element: <HomePage /> },
      { path: "products", element: <ProductsPage /> },
      { path: "products/:productId", element: <ProductDetails /> }
    ],
  },
]);

```

### Going to the previous page

If your relative attribute is set to route then your path would be relative to route In this way on cliking back you will go back to your parent route instead of one step back to the page from where you came here.

To deal this you have to set your relative to 'path' by doing this you will come back to where you are supposed to go
```bash
<p><Link to=".." relative="path">Back</Link></p>
```



### If you face error of unique key and get help from this below code:
```bash
import React from "react";
import { Link } from "react-router-dom";

const DUMMY_EVENTS = [
  { id: "e1", title: "Some Event"},
  { id: "e2", title: "Another Event"},
  { id: "e3", title: "An Another event"},
];
function EventsPage() {
  return (
    <ul>
      {DUMMY_EVENTS.map((event) => {
        return (
          <li key={event.id}>
            <Link to={event.id}>{event.title}</Link>
          </li>
        );
      })}
    </ul>
  );
}
export default EventsPage;
```


### Another example of app.js file
//here we are nesting the components you have same path within a path like all elements must have / and then must have /event
so why we write all these starting path address which is same. Here Rootlayout is parent of EventRootlayout and all inside them are their children

// Challenge / Exercise
```bash
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import HomePage from "./Pages/HomePage";
import RootLayout from "./Root";
import EventsPage from "./Pages/Events";
import EventDetailPage from "./Pages/EventDetailPage";
import NewEventPage from "./Pages/NewEventPage";
import EditEventPage from "./Pages/EditEventPage";
import ErrorPage from "./Pages/Error";
import EventsRootLayout from "./Pages/EventsRoot";

const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    errorElement: <ErrorPage/>,
    children: [
      { index: true, element: <HomePage /> },
      {
        path: "events",
        element: <EventsRootLayout />,
        children: [
          { path: "", element: <EventsPage /> },
          { path: ":eventId", element: <EventDetailPage /> },
          { path: "new", element: <NewEventPage /> },
          { path: ":eventId/edit", element: <EditEventPage /> },
        ],
      },
    ],
  },
]);
function App() {
  return (
    <>
      <RouterProvider router={router} />
    </>
  );
}

export default App;
```


### index attribute

This attribute is used to use to make your desired route a default route
to make you path default you to set index:true as:
```bash
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    errorElement: <ErrorPage />,
    children: [
      { index:true, element: <HomePage /> },
      { path: "products", element: <ProductsPage /> },
      { path: "products/:productId", element: <ProductDetails /> }
    ],
  },
]);
```


you can done the same by replacing index:true with path:''



### Outlet in react-router-dom

This <Outlet> is used to render the components which is nested inside the components defined above it


### Template of fetching data form backend
```bash
useEffect(() => {
    async function fetchEvents() {
      setIsLoading(true);
      const response = await fetch('http://localhost:8080/events');

      if (!response.ok) {
        setError('Fetching events failed.');
      } else {
        const resData = await response.json();
        setFetchedEvents(resData.events);
      }
      setIsLoading(false);
    }

    fetchEvents();
  }, []);

```

**NOTE:** its NOT a general template you always have to do some modifications while using it.

### useLoaderData Hook

This is a special hook which you execute to access the closest loader data

This hook will actually return the value of a loader function which we defined in our app.js inside the router function:

```bash
children: [
          {
            index: true,
            element: <EventsPage />,
            loader: loader
          },
          { path: ":eventId", element: <EventDetailPage /> },
          { path: "new", element: <NewEventPage /> },
          { path: ":eventId/edit", element: <EditEventPage /> },
        ]

//here loader function is in the event.js and we import it in app.js

export function loader() {
  return (
    async () => {
      const response = await fetch("http://localhost:8080/events");

      if (!response.ok) {
      } else {
        const resData = await response.json();
        const res = new Response('any data', {status: 201});
        return res;

      }
    }
  )
}

```

**Note** here the loader function in order get access to its data we use useloader hook. In <EventPage/> component.
**NOTE** we can only use our useLoader hook only on those component which are on the same level or on lower level. Always remember loader function is not a component its just a component. 

### useNavigation
This hook is used to get the current state of the event This hook is every useful for showing some loading... indicator
write
```bash
import React from "react";
import MainNavigation from "./components/MainNavigation";
import { Outlet, useNavigation } from "react-router-dom";

function EventsRootLayout() {
  const navigation = useNavigation();
  return (
    <nav>
      <MainNavigation />
      <main>
        {navigation.state === "loading" && <p>Loading...</p>}
        <Outlet />
      </main>
    </nav>
  );
}

export default EventsRootLayout;
```

### useRouteLoaderData

This hook is same as loader data but the difference is that this is used for using a loader function for a specific route in case there are more than loader functions. This can be done by this hook but to do so this hook requires an id as an argument.

### There is another hook called action function

as there is a loader to load data....There is alos a an action which is used to write as we know loader is used to read. Action function uses two arguments one is request and one is params.

If you want to trigger the action of other component in your current component you can do it by the below syntax:
```bash
<Form method="post" action="/songs" />;
```

here "/songs" is the path of other file

### redirect function
This special function is used to redirect the user to a specific page.
```bash
import {redirect } from 'react-router-dom'
const function(){
//you logic

return redirect('/your_Path_URL')
}
```
### useLoader() function
This function is to used load data before rendering the component
And remember this loader function will be created by us and it will an async function. This function fetch the data from the backend API usually in the form of JSON.

So simply create this function anywhere and then import it into App.js file
```bash
export const async myLoaderFunction = ()=> {	
	
	const res = await fetch('https://example.com/api/data')

 return res.json();

}
```
here note that .json() also returns a promise but dont need to worry about that as it will automatically handle by loader function

now you have to assosiate this loaderfunction to a route path. You can you do it by using loader property and by doing it so when ever you will visit that link this loader function is gonna execute and it will load the data before rendering the component. so during that time you have to show loading indicator
```bash
{ path="/products", element=<Product/>, loader: myLoaderFunction
}
```


once this path will be visited this myloaderFunction is gonna execute and on its execution it will do something which we have specified as in this case I have specified a fetch fuction which will fetch the data. So now we can use that returning data anywhere with the help of useLoader() hook.

simply import it 
```bash
import {useLoader} from 'react-router-dom';

function myComponent() {

	const data = useLoader();
}



```

**IMPORTANT** in which files this returning data will be avaiable?
SO that answer is that only in the file where you associate it with the path and its children components

**NOTE:** if there are several RouteloaderData hook and you want to call a specific loader function then you can use id: 'myID'
```bash
const data = useRouteLoaderData('myID)
```

### From and form actions

These both useLoader and actions work with createBrowserRouter only.

These <Form></Form> component in router 6.4 is extremely helpful once we submit the form it carries all the values into a bundle of JS objects and send it to the action function.
And again Action function is a function which we create ourselves it is bit like a loader function which was also created by us and fetch all the data and returns it. But this time we will get access to all the form data so we can do what we want with it. Like loader function action function will be called when the form will be submitted. This make working with from little bit easier

```bash
import {Form} from 'react-router-dom'
function myComponent() {
return (
	<Form method="Post" action="/path">
		<input type="email" name="email">Enter you Email</input> //dont forget to give name attributes to the input tag as they will be used to get values in obj.
	</Form>
)
}
```


when the form will be submitted the react will look for the action function React will go to the path defined in the action props and then there the action function associated with the specific route will be triggered. (created that action function anywhere and import it into app.js file and add it to the route
```bash
{ path="/products", element=<Product/>, action: myActionFunction
}
```


```bash
const export myActionFunction = async ({request}) => {
	console.log(request) //its a request object

	const data = request.formData()
	const submission = {
	email: data.get('email')
		}
	console.log(submission)
   if(submission.message.length > 250) {
	return {error: "Message must be less than 250 characters } // we can access this error object using useAction hook as this function is returning this error object
	}
   return redirect('/somePath')

}
```
- you always have to return something to action function
-  here request property will contain all the data entered by the user 
- here formData is a built in method which is used to access the data
- get method requires the name of the input field


- to get the data which this myActionFunction is returning can be get by using useAction hook

```bash
import {Form, useAction} from 'react-router-dom'
function myComponent() {
return (
const data = useAction();
	<Form method="Post" action="/path">
		<input type="email" name="email">Enter you Email</input> //dont forget to give name attributes to the input tag as they will be used to get values in obj.
	</Form>
)
}
```




### Navigate

This Component is simply used to redirect the user to the navigate page....its very important in case of you want to secure your data from the unauthenticated person

**for example**
```bash
import {Navigate} from 'react-router-dom'
if (!userloggedIn) {
	return <Navigate to="/path" replace={true} />

}
```


here replace attribute is very important cause once a user logged out and if he clicked on the go back button on browser it will again be logged in to the account as the account preserve the histroy so to prevent this behaviour we use replace={true	}

# 14 Authentication with React

### Query Parameter

query parameter is a parameter which appends in the URL aftter a question mark.

You can do authentication with the help of useState Hook but there is a web standard in which we do authentication uisng query parameter logic due to which this work easy to redirect to the authentication pages.

### useSearchParams
Query params are officially called search params
This hook actually returns an array
```bash
const [searchParams, setSearchParams] = useSearchParams();
const siLogin = searchParams.get('mode')

 <div className={classes.actions}>
          <Link to={`?mode=${isLogin ? 'signup' : 'login'}`} >
            {isLogin ? "Create new user" : "Login"}
          </Link>
```

- here mode is a keyword we used after ? we can set it to anyanem
- searchParams is an object of current query parameter
- here setSearchParams is a function to update searchParams




### Extra Info

```bash
fetch('https://localhost:8080/', {
    method : 'POST',
    header: {
      'Content-Type': 'application/json'
    },
    body:JSON.stringify(authData)
  })
```

These are some essentials must be set for post method

### Standard way of throwing errors
```bash
import {json} from 'react-router-dom'
if (!response.ok) {
    return json({message : 'Could not authenticate user'}, {status: 500})

  }
```
ٍٍٍٍٍبٍٍ
**Important**

***Important:** If doesn't return a value under certain circumstances.
then You should make sure that you do add an extra return null statement in all if statement branches where nothing would be returned otherwise to avoid errors.

# 15 React Animations
### Transition using CSS
We can hide or show our block using CSS
This can be simply done by creating two css classes one for showing and other for hiding

```bash
.myElement {
transition: all 0.3s ease-out;

}
.open{
opacity: 1;
transfrom : translateY(0);
}

.close
opacity: 0;
transfrom : translateY(-100%);

}
```


### Animation
you can apply animation using this syntax:
```bash
.myElement {
transition: all 0.3s ease-out;

}
.open{
animation: openModal 0.4s ease-out forwards;
}

.close
opacity: 0;
transfrom : translateY(-100%);

}
@keyframes openModal {

0% {
opacity: 0;
transfrom : translateY(-100%);
}

50% {
opacity: 1;
transfrom : translateY(20%);
}

100% {
opacity: 1;
transfrom : translateY(0);
}
}
```

### Limitations of css transition
The limitation is that  by using css transition....In case we hide our modal our modal do not get removed or hide from the DOM.
Its stays there but only thing changes its opacity. 


To solve this issue we can use ternary operation and render or remove element from DOM
but doing it so will wont have transitions and animations for out going. This can be solved by using some extra tools.

The tool is react transition group its a github repo you can use it.
https://github.com/reactjs/react-transition-group

```bash
import { Transition } from 'react-transition-group';
```

The main adv of this package is that this also manages the state.
on any state change it also provide an intermediate state so that we could perform our css transitions on them.
For example:
entering then entered
exiting then exited


after how much time it will entered or exited depends upon the time given in timeout.

**Example:**
```bash
 <Transition 
          in={this.state.showBlock} 
          timeout={1000}
          mountOnEnter
          unmountOnExit>
          {state => (
            <div
              style={{
                backgroundColor: "red",
                width: 100,
                height: 100,
                margin: "auto",
                transition: 'opacity 1s ease-out',
                opacity: state === 'exiting' ? 0 : 1
              }}
            />

// on exiting the transition will be shown
```

Here Transition tag comes with state which contains entering, entered, exititing, exited props


**Note:** always remember this time duration will be in mili seconds.


### Always remeber  CSS is add to React JS in the form of objects

```bash
style={{backgroundColor: 'red', width: 1}}
```

### Transition Methods	
These are the functions which will run on enter, entering etc.
```bash
<Transition 
          in={this.state.showBlock} 
          timeout={1000}
          mountOnEnter
          unmountOnExit
          onEnter={()=>console.log('Enter')}
          onEntering={()=>console.log('Entering')}
          onEntered={()=>console.log('Entered')}
          onExit={()=>console.log('Exit')}
          onExiting={()=>console.log('Exiting')}
          onExited={()=>console.log('Exited')}
          >
```


### Template Transitions
```bash
import { CSSTransition } from 'react-transition-group';
```

https://reactcommunity.org/react-transition-group/css-transition


### Transition Group

you can use it where you are outputing list
```bash
import {
  CSSTransition,
  TransitionGroup,
} from 'react-transition-group';
```


### Alternative package for animations
React Motion
https://github.com/chenglou/react-motion


React Move
https://github.com/sghall/react-move


**IMPORTANT**

Despite having such packages you should focus on CSS transitions 


# 16 Replacing Redux with React Hook
There is nothing wrong in using redux you can go with that
but what If you want to make an app without props and redux?
Then you can manage your state with react hooks.

There is no problem in using react redux but in case you want to update and manage your state but you dont want to use props and redux then there are two alternatives you can use to update and manage your state
That is react context API hook (not recommended)
To see how this work kindly go throught the advance event handling file
Link: https://drive.google.com/drive/folders/1LKQhfYI-ezPbZssjT_jL4oNDka5V3EAr


Why this context hook is not recommended. The reason is that this hook is not made for high frequency updates. Its basically for low frequency updates.

The other method is using custom hooks.

Again there is nothing wrong in using Redux. You can use it. It will do all heavy lifting for you.

# 17 Testing React App

This section is about automated testing.


### What is testing?
Till this stage we have done manual testing. Like debugging our code manually and previewing our application in browser and again test there manually.

But in case of automated testing all the code will be tested automatically no matters where you make changes in the code.

### Different types of tests
- Unite Tests (Testing the individual building blocks such as functions, code blocks or components)
- Integration Tests (Here we test the combination of multiple building blocks. Like one component is dependent on other component. Its not very common test. )
- End-to-End (e2e) Tests (This is the testing of entire scenario like the complete authentication system)


### Tool
- for runnig the test we use JEST  (JEST is not specific to react it is a general JS library)
- for rending our react app we use React Testing Library.
- there is anotoher library called React-hook testing library you can use them too.

Luckily both tools are already set up and when you install react app. There is no need to externally install them.

### JEST
To use testing we use: 
import '@testing-library/jest-dom';

The convention is that you must have to name you test file as you component file just add test name at the end.

### Pre-reqs

First create a test setup file namely setupTest.js in the src folder
```bash
//In setupTest.js
import '@testing-library/jest-dom';
```


Now create another file The convention is that you must have to name you test file as you component file just add test name at the end.
for example for testing App.js you have to create App.test.js
```bash
//now in App.test.js

import '@testing-library/jest-dom'
import { render, screen } from "@testing-library/react";
import App from "./App";

test("renders learn react link", () => {
  render(<App />);
  const linkElement = screen.getByText(/Learn React/i);
  expect(linkElement).toBeInTheDocument();
});

// and here if there is a component "Learn React" 
```
The test will run the component. Luckily its not case sensitive.

IMPORTANT: for the safe side you can install "npm i @testing-library/jest-dom"


Now to run test simple type:
```bash
> npm test
```
### Writing Custom test
To Wirte a custom test you have to follow some rules like 3 A's rule

1. Arrange (Setting test data, conditions and environment)
2. Act (Run logic that should be tested e.g. execute function)
3. Assert (Compare execution results with expected results)
```bash
//In Greeting.js file

import React from "react";

export default function Greeting() {
  return (
    <div>
      <h2>Hello World</h2>
      <p>
        Lorem, ipsum dolor sit amet consectetur adipisicing elit. Adipisci porro
        illum, est ut quam possimus iure iusto corrupti praesentium minima sit
        suscipit, aliquid vel. Animi minima error distinctio amet labore.
      </p>
    </div>
  );
}


```
```bash
// In Greeting.Test.js file


import Greeting from "./Greeting";
import { render, screen } from "@testing-library/react";

test('Render Hellos world as text', ()=>{
    // Arrange
    render(<Greeting/>);

    //Act 
    // (But here act is nothing)

    //Assert
    const helloWorldElement = screen.getByText('Hello World', {exact: false});
    expect(helloWorldElement).toBeInTheDocument();
}); 
```

here test is the built in function which will be run on running the test. It takes two argument one is the name or sentence about test and a callback function.
//here screen is like virtual DOM 
//here exact: false will give us leniency in matching the text.
//where as if exact: true will match exactly event the full stop :)
### Wiritng test for greeting file

**Extra info**
```bash
here .get() method shows error on finding the value
.query() this do not throw any errors
.find() this method returns a promise.
```


### how to group mulitple test
for grouping test you have to make suits using describe function
```bash
import Greeting from "./Greeting";
import { render, screen } from "@testing-library/react";

describe("Greeitng component", () => {
  test("Render Hellos world as text", () => {
    // Arrange
    render(<Greeting />);

    //Act
    // (But here act is nothing)

    //Assert
    const helloWorldElement = screen.getByText("Hello World", { exact: false });
    expect(helloWorldElement).toBeInTheDocument();
  });
test('your logic');
test('your logic');
test('your logic');
});

```

here you can run multiple tests inside describe function.



### Test for states
```bash
//In Greeting.js Component

import React from "react";
import { useState } from "react";
export default function Greeting() {
  const [changeText, setChangeText] = useState(false);
  const changeTextHandler = () => {
    setChangeText(true);
  };
  return (
    <div>
      <h2>Hello World</h2>
      {!changeText && <p>Its good to see you.</p>}
      {changeText && <p>Changed!</p>}
      <button onClick={changeTextHandler}>Change</button>
    </div>
  );
}
```
```bash
// In Greeting.test.js

import Greeting from "./Greeting";
import userEvent from "@testing-library/user-event";
import { render, screen } from "@testing-library/react";

describe("Greeitng component", () => {
  test("Render Hellos world as text", () => {
    // Arrange
    render(<Greeting />);

    //Act
    // (But here act is nothing)

    //Assert
    const helloWorldElement = screen.getByText("Hello World", { exact: false });
    expect(helloWorldElement).toBeInTheDocument();
});
test('Renders good to see you if the button was NOT clicked', ()=> {
    //Arrange
    render(<Greeting/>);
    //Act
    // (But here act is nothing)
    
    //Assert
    const outputElement = screen.getByText("Its good to see you", { exact: false });
    expect(outputElement).toBeInTheDocument();

  });
test('Renders Changed! if the button was click', ()=> {
    //Arrange
    render(<Greeting/>);
    //Act
    const buttonElement = screen.getByRole('button');
    userEvent.click(buttonElement)  
    
    //Assert
    const outputElement = screen.getByText("Changed!", { exact: false });
    expect(outputElement).toBeInTheDocument() ;

  });
});
```

//here screen is like virtual DOM
//here exact: false will give us leniency in matching the text.
//where as if exact: true will match exactly event the full stop :)


//Here screen is DOM and here its not an HTML or windows DOM its a DOM of React component on which are running our test. This is like so that we can access our React component element and write rest for them



### Precautions
while working test with async code in which we are sending request to the servers to fetch the data. Its not be done. Like while testing we should NOT send request to server. Or we should send request to a fake test server.
Always remember. You have to run test on functions which are written by you. Like you dont have to run tests for built in functions like fetch() cause we trust the react developer and testing a function simply means whether it is working as expected or not. SO for built in functions we believe that they are already tested from the React Developers and there is no need to test them. We are only responsible for the functions which we have written by ourselves

But how can we replace fetch with a dummy function?
```bash
fetch('url').then(response => response.json()).then(data => console.log(data));
```
//simply to make the above function a mock or dummy function replace it by below:
```bash
window.fetch = jest.fn();
window.fetch.MockResolvedValueOnce({json: async()=> [{id: 'p1', title:'First post'}]})
```
in this way we are not sending any request to the real server instead we are using our mock function and its behaviour is controlled. 
By mocking the fetch function, you can control its behavior and simulate responses without actually making network requests. This is particularly useful during testing, as it allows you to isolate and test specific parts of your code without relying on external APIs or making actual network calls.
# 18 Preventing Unnecessary execution 
### React.memo()
memo from memory 
This function prevent the unnecessary re-execution of the react component. This hook compares the value of props with the previous props it will allow the re-execution only when there is a change in the value of props. If the value is not change then the re-execution for this component will be skipped. In this way we can optimize our React App


**IMPORTANT:** If its is so, then we dont use React.memo on all components? 
The Answer is that this React.memo comes with a cost like React must have to store it the previous value and then compare it with the new value. In this way the React have to do two things one storing the value and second one is to comparison. This will also effect the performance of React App.

But one more important thing to remember is that a regular function calling multiple time will be treated as the new value. As we know that functions are objects and two object/arrays will have the same value will not be equal. 
For exp: 
```bash
[1,2,3]===[1,2,3] //flase and f()=== f()  //false
```
So this means that React.memo()  is useless for objects? cause it is unable to compare the objects despite having the fact that objects are same?
Answer is NO. To make memo useful we use an extra hook called.  useCallback()

### useCallback() 
This hook allows us to save functions so that they could not be re-created and will have the same address in memory so that the comparison operator could work correctly.
```bash
import {useCallback} from 'React';

useCallback(function, dependencies)
```

this hook takes a fucntion as a first argument which we want to save and its dependencies as the second argument.

So we can use useCallback() hook on such functions about which we are sure that this function will not be changed

its dependencies are same as useEffect function. 

You can raise a question that on one side we say that 	we can use useCallback() hook on such functions about which we are sure that this function will not be changed and on the other hand we ask for dependencies. WHHHYYYY???? dependencies are needed only when you are sure that this thing will change in future. But why are we using dependencies with useCallback() argument function about which we are sure that not gonna change.

The answer is closure. The functions are closures in javaScript. Means that the variables inside this functions are coming from outside of the function may change. And function remember that value and on calling the same function again the value will be updated. Therefore we have to tell the useCallback() that dont re-create this function at any circumstances BUT re-create it only when the variable given in the depencies will change......In short we add variables in dependencies in useCallback() function to create come exceptions fro re-creating the functions.


**IMPORTANT:** Since the component is re-evaluted doesn't it mean that we are re-initializing our state again and again?
Answer is NO. Since we know that react is responsible for managing our state and components. This management process will not consider the useState() while re-evaluating casue useState is coming from react and it make sure that the useState() will not re-initialize.


### React Schedule and Batch execution

Whenever we make changes in our app. React do not change it instantly but it postponed the state change or may be schedule tha state. React also have priority precedence. Like it will highly prioritize the input getting from user and so on.

**IMPORTANT:**
Since we have discussed that React schedule the state updates so there is a possibility that more than one state is managed at the same time. Therefore, we use callback function inside setState function where one state is dependant on the previous state so that more than one event don not schedule at the same time.

In short React do not instantly update the state it schedule the state management.
This is the reason we do not get the latest state earlier. We get that state when the component will re-render/Re-evaluated.



Other case: if there is a case like in which a regular function we are running two setState functions line by line then React will execute both of them in Batch.



### useMemo() Hook
This hook is same as useCallback() hook but the difference is that useMemo() memoize the data whereas useCallback memoize the function. 
useCallback is more usefull than useMemo. 
In short : useCallback returns a memoized callback function, while useMemo returns a memoized value.
```bash
import {useMemo} from 'React';

useMemo(function, dependencies)
```


**For Example:** there is an expression or loop which a function is return a value that may take some time in execution if the loop is large. So if that expression is not changing then why is there any need to re-evaluate that or call that function again and again on every execution. This may lead to compromise on performance. So in order to store the value of that calculation or loop we use useMemo() Hook so that in case of not changing in its value it skip its re-evalution.

# 19 Rules of Hooks
- Only call Hooks in React Component Functions. You cannot call hook functions outside the component function.
- Dont call them in nested function. or in block code.
- Specifil unofficail rule for useEffect():
- Always add every thing in you dependencies that you have refered in the useEffect callback function.

