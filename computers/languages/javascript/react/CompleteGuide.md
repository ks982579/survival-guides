# React - Complete Guide

So, other notes are in MS word. Hoping to eventually migrate notes over to markdown. 

- [ ] Finish Udemy Course
- [ ] Migrate Notes

## Section 15: Building Custom React Hooks

### Lesson 185: Module Introduction

So far, we have been working with the built-in React hooks. Just to recap the rules of React Hooks:
- Only call React Hooks in React Functions.
	- React component functions
	- **In Custom Hooks**
- Only call hooks at the top level.
	- Do not call in nested functions.
	- Do not call them in block statements. 

An an _unofficial_ rule for `useEffect()` is to **always** add everything you refer to inside the hook as a dependency. 

Things to discuss:
- What are custom hooks?
- Why do we need them?
- How do we build and use them?
- What are custom hook rules and best practices?

### Lesson 186: What are "Custom Hooks"?

Custom hooks are regular functions just like the built-in React hooks. However, they are functions that can contain **stateful** logic. Unlike "regular functions", custom hooks can use other React hooks and React state. They are bits of re-usable logic that can benefit from React's built-in hooks. 

### Lesson 187: Creating a Custom React Hook Function

There's an example project with this lesson. There are two main components that count up and down each second respectively. Because the components are so similar, it is safe to say there is code duplication. 

Typically when we have code duplication, we want to abstract it into a function (or something similar) to improve readability and scalability. However, our components require using React hooks, like `useEffect()` and depend on state. Since we cannot use hooks in ordinary functions, we need to outsource them to custom hooks. 

To get started, let's create a custom hooks directory and file, `/src/hooks/use-counter.js`. You can name the file what you want, but the rule about hooks is they **must** begin with the word "use". This signals to React that our function is a custom hook, and allows the React to monitor its use. So, if we violate any rule of hooks, we should get warning ahead of time. 

For our example, we are going to copy the logic out of one of the similar components. 

```js
import  React, {useState, useEffect} from  'react';

const  useCounter = () => {
	const [counter, setCounter] = useState(0);
	
	useEffect(() => {
		const  interval = setInterval(() => {
			setCounter((prevState) =>  prevState + 1);
		}, 1000);
		return () =>  clearInterval(interval);
	}, []);

	return counter;
};

export  default  useCounter
```

Note, we will also return the `counter`. The hook is like a regular function, or you can think of it like `useState()`. The component we will use this in will require this value, so we must return it. 

This is only what we have so far. 

### Lesson 188: Using Custom Hooks

We must import them like we would a regular hook, just from their relative location instead of from 'react'. In our example, we will import the hook into our `<ForwardCounter/>` component. 

First, let's just look at what we would have had to do without a custom hook:

```js
import React, { useState, useEffect } from  'react';
import  Card  from  './Card';
import  useCounter  from  '../hooks/use-counter';

const  ForwardCounter = () => {
	const [counter, setCounter] = useState(0);

	useEffect(() => {
		const  interval = setInterval(() => {
		setCounter((prevCounter) =>  prevCounter + 1);
	}, 1000);
	
	return () =>  clearInterval(interval);
	}, []);
	
	return  <Card>{counter}</Card>;
};

export  default  ForwardCounter;
```

It's basically the `useCounter()` hook logic, just unpacked in the component. Now, let's use our custom hook:

```js
import  React  from  'react';
import  Card  from  './Card';
import  useCounter  from  '../hooks/use-counter';

const  ForwardCounter = () => {
	const  counter = useCounter();
	
	return  <Card>{counter}</Card>;
};

export  default  ForwardCounter;
```

As seen above, you can call the hook in our component like a regular built-in React hook. Important to remember that if your custom hook has state or effects within it, then those will be tied to the component(s) you call the hook in.  Suppose just to be clear, if you call the hook in multiple components, they will __not__ share the same state. Each one gets its own state in reference to the hook. 

It keeps the components a bit smaller, more slim.

### Lesson 189: Configuring Custom Hooks

We are now going to look at our `<BackwardCounter />` component. It is similar logic, but our component counts down instead of up. We don't want to create a separate custom hook with very similar logic, but rather make the current hook configurable by accepting arguments. Consider the built-in `useState()` hook, which can take in an initial state. 

We _could_ go as far as to allow a user to pass in an entire function to determine how the counter is updated each second. But, we will settle for just a flag as our custom hook doesn't need to be that flexible. Our flag will run through a conditional statement to determine how state is changed. 

```js
import React, {useState, useEffect} from 'react';

const useCounter = (countForwards = true) => {
    const [counter, setCounter] = useState(0);

    useEffect(() => {
        const interval = setInterval(() => {
            if (countForwards) {
                setCounter((prevState) => prevState + 1);
            } else {
                setCounter((prevState) => prevState - 1);
            }
        }, 1000);

        return () => clearInterval(interval);
    }, [countForwards]);

    return counter;
};

export default useCounter
```

Notice that our `useEffect()` gained an external dependency. For now, we don't expect the dependency to change, but it's still good practice to list dependencies. 

And here is the `<BackwardCounter />` component:

```js
import React from 'react';
import useCounter from '../hooks/use-counter';

import Card from './Card';

const BackwardCounter = () => {
  const counter = useCounter(false);

  return <Card>{counter}</Card>;
};

export default BackwardCounter;
```

### Lesson 190: Onwards To A More Realistic Example

This lesson begins with a new example project. It requires a backend, so you can add your own firebase links. Using the _Realtime Database_ service, we would set the following rules:

```json
{
	"rules": {
		".read": true,
		".write": true
	}
}
```

You want to use your own URL, but add on the `...firebaseio.com/tasks.json` so that the information is saved in a `tasks.json` file. 

This is just a task application. The `<App />` component fetches information from the backend and runs it through others to display the information. We store data by sending a POST request. 

Currently, each component handles its own http requests. But this is a good opportunity to create a configurable custom hook. Even though there are differences with sending GET and POST requests, there are many similarities. For example, they both handle loading and error handling states, things _Axios_ may do for you. Since we have duplicate logic, we want to abstract some of it away in a function. But because the logic requires hooks like `useEffect()` and `useState()`, we can't use a regular function, it must be a custom hook. 

### Lesson 191: Building a Custom HTTP Hook

A good start is to add a `/app/src/hooks/` directory, same level as the "components" directory. It's common convention. We then create a file, `/app/src/hooks/use-http.js`. The function we create will be "useHttp", and must begin with the word "use". The component needs state for loading and errors. 

We want to design the hook to be quite generic, not just specific to fetching tasks. We want to fetch any kind of data from any kind of URL, and make any kind of transformations. That will require parameters. Below is a pretty good approach. 

```js
import React, { useState, useEffect } from 'react';

const useHttp = (requestConfig, applyData) => {
    /** Params:
     *      requestConfig - object to configure fetch API
     *          url - URL to send request to
     *          method - GET or POST
     *          headers - 
     *          body - JS object
     */
    const [isLoading, setIsLoading] = useState(false);
    const [error, setError] = useState(null);

    const sendRequest = async (taskText) => {
        setIsLoading(true);
        setError(null);
        try {
            const response = await fetch(
                requestConfig.url, {
                    method: requestConfig.method,
                    headers: requestConfig.headers,
                    body: JSON.stringify(requestConfig.body)
                }
            );

            if (!response.ok) {
                throw new Error('Request failed!');
            }

            const data = await response.json();
            applyData(data);

        } catch (err) {
            setError(err.message || 'Something went wrong!');
        }
        setIsLoading(false);
    };

    return {
        isLoading,
        error,
        sendRequest
    }
}

export default useHttp;
```

We handle all of the arguments of the fetch API with a `requestConfig` object. We also handle errors and receiving JSON data. Although we want the hook to be flexible, accepting other data types is beyond the scope of this course. We also take in a function to transform the data. This allows the component that is using the hook to configure the output to its specifications. 

Now, we have many values that the component using the hook will need access to. That is why we are returning the object of values. 

### Lesson 192: Using the Custom Http Hook

In the `<App/>` component, we can import our hook and remove logic that it replaces. We also need to pass in the required arguments. For the GET request, we don't need any header or a body, and the default method is GET for the `fetch()` API. 

However, in the spirit of type checking, we can implement some data checks in the `use-http.js` file:
```js
try {
    const response = await fetch(
        requestConfig.url, {
			method: requestConfig.method ? requestConfig.method : 'GET',
			headers: requestConfig.headers ? requestConfig.headers : {},
			body: requestConfig.body ? JSON.stringify(requestConfig.body) : null
        }
    );
```

That just allows for the object to be flexible itself. 

We also need to add a function, which the logic can be found in the component. Remember that the custom hook also returns values. 

```js
import React, { useEffect, useState } from 'react';

import Tasks from './components/Tasks/Tasks';
import NewTask from './components/NewTask/NewTask';
import useHttp from './hooks/use-http';

function App() {
  const [tasks, setTasks] = useState([]);
  requestConfig = {
    url: 'https://react-http-6b4a6.firebaseio.com/tasks.json',
  }

  const transformTasks = (taskObj) => {
    const loadedTasks = [];

    for (const taskKey in taskObj) {
      loadedTasks.push({ id: taskKey, text: taskObj[taskKey].text });
    }

    setTasks(loadedTasks);
  }

  const httpData = useHttp(requestConfig, transformTasks);
  const { isLoading, error, sendRequest: fetchTasks } = httpData;

  useEffect(() => {
    fetchTasks();
  }, []);

  const taskAddHandler = (task) => {
    setTasks((prevTasks) => prevTasks.concat(task));
  };

  return (
    <React.Fragment>
      <NewTask onAddTask={taskAddHandler} />
      <Tasks
        items={tasks}
        loading={isLoading}
        error={error}
        onFetch={fetchTasks}
      />
    </React.Fragment>
  );
}

export default App;
```

This isn't complete because we aren't using the `useEffect()` hook in the best practices kind of way. 

### Lesson 193: Adjusting Custom Hook Logic

We want our code to follow best practices, but if we put the `fetchTasks()` function as a dependency in the `useEffect()` hook, it will cause an infinite loop. Basically, the state in the custom hook changes and causes the component to re-render. That calls the custom hook again, which re-creates the `sendRequest()` function... 

To fix this, we can wrap the function in our custom hook in the `useCallback()` hook. 

```js
import React, { useState, useCallback } from 'react';

const useHttp = (requestConfig, applyData) => {
    ...
    const sendRequest = useCallback(async (taskText) => {
...
```

Recall that the `useCallback()` hook also takes in a dependency array. However, both `[requestConfig, applyData]` are objects passed in through the `<App/>` components, so we must ensure they are not excessively recreated. 

That means we wrap our `transformTasks()` function in `useCallback()`, which uses state as an external dependency, but React guarantees that to remain constant. 

Let's think about how to prevent the `requestConfig` object from re-rendering. We could use the `useMemo()` hook, or we can rework our `useHttp()` hook. 

```js
...
  const requestConfig = useMemo(() => {
    return ({
      url: 'https://react-http-6b4a6.firebaseio.com/tasks.json'
      }
    )
  }, []);
...
```

The second way is to actually have all the arguments passed into the `sendRequest()` function that is returned from the hook. Then, we can create and pass both of those values into the function inside of the `useEffect()` hook, which will eliminate the re-rendering. This method minimizes dependencies, but the logic can be more complicated. 

This leads to an interesting lesson, the sooner you introduce objects into your code, the longer you have to manage them. So, to reduce complexity we can introduce objects and information only when required. 

### Lesson 194: Using the Custom Hook in More Components

We also want to create new tasks with a component using our custom hook. This is in `/app/src/components/NewTaks/NewTask.js`. We start by importing our custom hook, and then calling it in the component. We also store its outputs in variables. 

The function `enterTaskHandler()` is called when the user submits a form. We want to run our `sendRequest()` function, returned by our custom hook, when the form is submitted. Since we are sending a POST request, we have to fill in some additional information. 

There is an interesting problem that arises. We want to pass in the text that we get from the form into the hook's generated function. But it only accepts json data returned by the request, which in a POST request case could just be 'OK'. 

We can use the `.bind()` method to bind the value to our function/object. The `bind()` method works on all objects. The first parameter is the object to define as `this`. The other parameters will be what is also passed into the function. Remember, this is a pre-configuration, so the data passed in naturally gets passed in after the `bind()` method passes in information. 

More information about `bind` can be found in this [Academind article](https://academind.com/tutorials/function-bind-event-execution). 

```js
import React from 'react';

import Section from '../UI/Section';
import TaskForm from './TaskForm';
import useHttp from '../../hooks/use-http';

const NewTask = (props) => {
  const httpData = useHttp();
  const { isLoading, error, sendRequest: sendTaskRequest } = httpData;

  const createdTask = (taskText, taskData) => {
    const generatedId = taskData.name; // firebase-specific => "name" contains generated id
    const createdTask = { id: generatedId, text: taskText };

    props.onAddTask(createdTask);
  }

  const enterTaskHandler = async (taskText) => {

    sendTaskRequest({
      url: 'https://react-http-6b4a6.firebaseio.com/tasks.json',
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: { text: taskText }
    }, createdTask.bind(null, taskText));
  };

  return (
    <Section>
      <TaskForm onEnterTask={enterTaskHandler} loading={isLoading} />
      {error && <p>{error}</p>}
    </Section>
  );
};

export default NewTask;
```

## Section 16: Working w/Forms and User Input

### Lesson 196: Module Introduction

Let's talk about forms and handling user input. It might sound trivial, but many web applications are all about forms and capturing user input. It may also be more difficult to provide useful feedback to the user while they fill out forms, for incorrect values and such. 

We won't touch on new React features, but cover the following:
- What is complex about forms?
- How to handle inputs and Forms with React.
- Tools and approaches to simplify the process.

### Lesson 197: Our Starting Setup

The starter project is just a simple form that takes in a name. We will not talk about HTML and CSS, those are provided and assumed. 

### Lesson 198: What is so complex about forms?

Forms can be complex because they, and their inputs, can assume different states. Examples are...

```mermaid
flowchart TD
A(Form and Inputs)
B(One or more inputs invalid)
C(All inputs are valid)
A ---> B
A ---> C
```

States may also be unknown if the checking is asyncronous. Suppose you need to send information to a server, like an email, to determine if it is valid, or already exists. 

However, we can think of the sum of the states within the form make up the form's state. When there are errors, we as developers want to output **input-specific** error messages and highlight problematic inputs. We also must ensure the form cannot be submitted or saved if it has errors. 

Things get more complex when we try to dive into displaying error messages. The question becomes when to validate user input? 
- When the form is submitted?
- When the input loses focus?
- On every keystroke?

Each has its pros and cons. If we check the form as a whole, we allow the user to enter invalid values before warning them. It's good because we aren't jumping the gun, giving warning before they are even done typing. It avoids unnecessary warnings but may present feedback "too late". That may not be the greatest user experience. 

When we validate after an input loses focus, we allow the user to finish typing their input before validation, again not jumping the gun. And we provide feedback in a timely manner, when they are done providing information. Very useful approach for _untouched_ forms. The downside is that if the user has made a mistake, we cannot tell them whether their new input is correct until after they finish typing again. 

That is where validation on keystroke can be handy. You provide feedback to a user on every keystroke, checking if the input is valid. The biggest downside to warning a user before they have had a chance to finish typing. So, you might see a lot of errors, which is not a great UX. However, if this approach is only applied on invalid inputs, it has the potential of providing direct feedback. 

### Lesson 199: Dealing with form submissions and getting user input

We currently have a `<SimpleInput/>` input component. 

```js
const SimpleInput = (props) => {
  return (
    <form>
      <div className='form-control'>
        <label htmlFor='name'>Your Name</label>
        <input type='text' id='name' />
      </div>
      <div className="form-actions">
        <button>Submit</button>
      </div>
    </form>
  );
};

export default SimpleInput;
```

It currently has no state to validate input. We can capture input with a `ref` to check input when the user is done typing, or useState to view input on every keystroke. We will start with catching every keystroke. 

Import `useState` and create the state. We then have to add an event listener to the `<input/>` element that changes state. The event listener, per vanilla JavaScript, will receive an `event` object by default that holds the values we need. We will actually bind the event listener to the `onChange` event listener, as it is better than key-down or key-up. 

We also need an event listener for the form submission so we prevent the page from re-rendering. We call `event.preventDefault();` on the event listener, and bind it to the `onSubmit` event listener of the `<form/>` element. We will also just log the name to the console just to show the updates so far. 

Updates:
```js
import React, { useRef, useState } from 'react';

const SimpleInput = (props) => {
  const [enteredName, setEnteredName] = useState('');

  const nameInputChangeHandler = event => {
    setEnteredName(event.target.value);
  }

  const formSubmissionHandler = event => {
    event.preventDefault();

    console.log(enteredName);
  }

  return (
    <form onSubmit={formSubmissionHandler}>
      <div className='form-control'>
        <label htmlFor='name'>Your Name</label>
        <input type='text' id='name' onChange={nameInputChangeHandler}/>
      </div>
      <div className="form-actions">
        <button>Submit</button>
      </div>
    </form>
  );
};

export default SimpleInput;
```

What about the `useRef` approach? Create a `ref` with the hook and set the ref inside the `<input />` element. We can then read the value from the `refObject.current.value;` property. 

```js
import React, { useRef, useState } from 'react';

const SimpleInput = (props) => {
  const nameInputRef = useRef();

  const formSubmissionHandler = event => {
    const enteredValue = nameInputRef.current.value;
    console.log(enteredValue);
  }

  return (
    <form onSubmit={formSubmissionHandler}>
      <div className='form-control'>
        <label htmlFor='name'>Your Name</label>
        <input ref={nameInputRef} type='text' id='name' />
      </div>
...
```

So, here we are just looking at the `ref` when the form is submitted. 

Don't forget that we can also set the value of the `<input ... value={enteredName}/>` element to the value of the state, which is not something we really want to do with `ref`. Then, when the form is submitted, we can capture the value and reset it to an empty string. We could also set the value of `ref` for a similar effect, but we shouldn't be directly manipulating the DOM. 

Now that we have covered how to get user input, we can dive into validation. 

### Lesson 200: Adding Basic Validation

Browser validation is great, but must not be the only validation performed as users can manipulate JavaScript in the browser and get around validations, sending what they want to the server. JavaScript is not reliable because the user can change it and is not a security mechanism. It's there to provide a good UX. 

The instructor provides an additional article, [Hide JavaScript Code](https://academind.com/tutorials/hide-javascript-code). 

First use case of data validation is to not send empty data to the server. We can add an `if` check in our form submission handler. It's always good to call the `trim()` function on strings as well to remove extra spaces. 

```js
...
  const formSubmissionHandler = event => {
    event.preventDefault();

    if (enteredName.trim() === '') {
      return;
    }

    console.log(enteredName);
  }
...
```

This is good because we now caught the error. But from the user's side, they don't know that nothing happened. We need to provide them with feedback. 

### Lesson 201: Providing validation feedback

We will bind input validation messages to state, and render message if the state is false... or true depending on how you work it. For this example, the state is for the input being valid, so it begins with an initial value of false. 

This means when we check for valid input, we also change state. Now, we can use the state to conditionally render a message. 

```js
import React, { useRef, useState } from 'react';

const SimpleInput = (props) => {
  ...
  const [enteredNameIsValid, setEnteredNameIsValid] = useState(false);
  ...
  const formSubmissionHandler = event => {
    event.preventDefault();

    if (enteredName.trim() === '') {
      setEnteredNameIsValid(false);
      return;
    }

    setEnteredNameIsValid(true);

    console.log(enteredName);
  }

  return (
    <form onSubmit={formSubmissionHandler}>
      <div className='form-control'>
        <label htmlFor='name'>Your Name</label>
        <input type='text' id='name' onChange={nameInputChangeHandler}/>
        {!setEnteredNameIsValid && <p className='error-text'>Name must not be empty.</p>}
      </div>
      ...
```

The current issue with this is that the error message is displayed before the user enters any information. A quick fix is to set the initial `isValid` state to true. Probably more on this later. 

First, let's talk about conditional CSS, so we can render our form a different colour if an input is invalid. It's as simple as putting the logic into a dynamic variable. 

```js
...
  const nameInputClasses = enteredNameIsValid ? 'form-control' : 'form-control invalid';

  return (
    <form onSubmit={formSubmissionHandler}>
      <div className={nameInputClasses}>
        <label htmlFor='name'>Your Name</label>
...
```


### Lesson 202: Handling the "was touched" state

Now, back to the blatant lie we tell ourselves that our form is valid from the start. It may seem harmless, but incorrect logic always has a way of creating issues at some point. Think of a `useEffect` that does something when the input is valid, like makes a call to the database to check if an email exists. That will now run as soon as the application starts because of the incorrect state. 

We will create another state to determine if the user has entered any input. We can then create our own validation variable that is the value of both the `!enteredNameIsValid && enteredNameTouched`. Then, we can use that Boolean value throughout the rest of our component. 

**Word of Caution**: Make sure the code matches your Boolean values. In our example, we changed the value to a check of invalidity (for some reason). 

The final step is handling how we change the `isTouched` state. 

```js
import React, { useRef, useState } from 'react';

const SimpleInput = (props) => {
  const [enteredName, setEnteredName] = useState('');
  const [enteredNameIsValid, setEnteredNameIsValid] = useState(false);
  const [enteredNameTouched, setEnteredNameTouched] = useState(false);

  const nameInputChangeHandler = event => {
    setEnteredName(event.target.value);
  }

  const formSubmissionHandler = event => {
    event.preventDefault();

    setEnteredNameTouched(true);
	...
  }

  const nameInputIsInvalid = !enteredNameIsValid && enteredNameTouched;
  const nameInputClasses = nameInputIsInvalid ? 'form-control invalid' : 'form-control';

  return (
    <form onSubmit={formSubmissionHandler}>
      <div className={nameInputClasses}>
        <label htmlFor='name'>Your Name</label>
        <input type='text' id='name' onChange={nameInputChangeHandler}/>
        {nameInputIsInvalid && <p className='error-text'>Name must not be empty.</p>}
      </div>
...
```

In our case, we decided to check on form submission. When the form is submitted, we will consider input to have been touched, and it cannot be untouched. 

Although it looks like more code, it reads better, is cleaner, and allows us to handle more use cases. 

### Lesson 203: React to Lose Focus

Where does our `onSubmit` check fail? A user can click into the form, enter some information, delete it all, and try to send an empty input. They aren't allowed to send empty input, but they aren't told about the error until after they click "Submit". A better UX might be to warn the user when they leave the input box, or `onBlur` for components. 

We must add a new event listener function and bind the function to the `<input />` element. Inside the event handler function, we want to set the `wasTouched` state to true. We also want to add our validation logic, which is currently just ensuring the input isn't blank. 

```js
import React, { useRef, useState } from 'react';

const SimpleInput = (props) => {
...
  const nameInputChangeHandler = event => {
    setEnteredName(event.target.value);
  }

  const nameInputBlurHandler = event => {
    setEnteredNameTouched(true);

    if (enteredName.trim() === '') {
      setEnteredNameIsValid(false);
    }
  }

  const formSubmissionHandler = event => {
...

  return (
    <form onSubmit={formSubmissionHandler}>
      <div className={nameInputClasses}>
        <label htmlFor='name'>Your Name</label>
        <input type='text' id='name' onChange={nameInputChangeHandler} onBlur={nameInputBlurHandler}/>
...
```

The above example cuts out some bits of the component. Basically, adding the `onBlur` now can show error messages. However, we might want to remove the error message once the user starts typing again. This is where we will combine lost focus validation with keystroke validation for the best UX.

### Lesson 204: Refactoring and Deriving State

We want to reuse our `onChange` event handler function to check validity of input on each keystroke. We currently have checks for if the input is invalid. However, this will call for checking if the input is valid, and only after being touched. 

```js
...
  const nameInputChangeHandler = event => {
    setEnteredName(event.target.value);

    if (event.target.value.trim() !== '') {
      setEnteredNameIsValid(true);
    }
  }
...
```

You'll notice some subtle differences, such as checking the event value instead of the state value. This is because state changes may not be instantaneous, and we don't want to validate old state. We also didn't set the keystroke check to only check when `isTouched = true`. That's ok I guess. 

This might be a better user experience, but our code isn't great. Our component is quite bloated. First, clean up an references to the `useRef` hook if you haven't already. 

We can also remove the `enteredNameIsValid` state, and derive a variable whose value is determined by the input value `enteredName`. Because the `enteredName` state is tied to every keystroke, we can ensure the variable we create will also be updated on state changes. This means we can remove calls to change the `enteredNameIsValid` state, which was in every event handler. 

We should also regroup our "inferred" states, the variables we are treating like state, which are derived from state, to the top. 

The form submission handler is slightly different. We can't remove the check, but since we have already updated the state, we can just check the state and not update it. 

We are also going to reset the state if, and only if, the form submits. But we also need to set the `isTouched = false` so errors don't populate after resetting the input. 

```js
import React, { useState } from 'react';

const SimpleInput = (props) => {
  const [enteredName, setEnteredName] = useState('');
  const [enteredNameTouched, setEnteredNameTouched] = useState(false);

  const enteredNameIsValid = enteredName.trim() !== '';
  const nameInputIsInvalid = !enteredNameIsValid && enteredNameTouched;

  const nameInputChangeHandler = event => {
    setEnteredName(event.target.value);
  }

  const nameInputBlurHandler = event => {
    setEnteredNameTouched(true);
  }

  const formSubmissionHandler = event => {
    event.preventDefault();

    setEnteredNameTouched(true);

    if (!enteredNameIsValid) {
      return;
    }
    console.log(enteredName);
    setEnteredName('');
    setEnteredNameTouched(false);
  }

  const nameInputClasses = nameInputIsInvalid ? 'form-control invalid' : 'form-control';

  return (...
```

Now that the component has been refactored, it is a bit leaner. We also practiced working with **inferred state**, or **derived state**.  

### Lesson 205: Managing the Overall Form Validity

So far, we have been validating input from one input element. However, it is usually also beneficial to know whether the overall form, composed of many elements, is also valid. Usually, a form is only valid if all inputs are also valid. 

How can we do this? We can create a `formIsValid` state, with an initial value of `false`. We want to update this state when an input is updated. We can actually accomplish this with the `useEffect` hook. And our `useEffect` hook will depend on the input component's validity state, or the _derived state_. 

Basically, in the hook, we want to check all validity states, and set the overall form validity state accordingly. 

```js
import React, { useEffect, useState } from 'react';

const SimpleInput = (props) => {
  const [enteredName, setEnteredName] = useState('');
  const [enteredNameTouched, setEnteredNameTouched] = useState(false);
  const [formIsValid, setFormIsValid] = useState(false);

  const enteredNameIsValid = enteredName.trim() !== '';
  const nameInputIsInvalid = !enteredNameIsValid && enteredNameTouched;

  useEffect(() => {
    if (enteredNameIsValid){
      setFormIsValid(true);
    } else {
      setFormIsValid(false);
    }
  }, [enteredNameIsValid]);
...
```

Now, we can actually use this state to disable the submit button when the form is not valid. 

```js
...
  return (
    <form onSubmit={formSubmissionHandler}>
      <div className={nameInputClasses}>
        <label htmlFor='name'>Your Name</label>
        <input type='text' id='name' onChange={nameInputChangeHandler} onBlur={nameInputBlurHandler}/>
        {nameInputIsInvalid && <p className='error-text'>Name must not be empty.</p>}
      </div>
      <div className="form-actions">
        <button disabled={!formIsValid}>Submit</button>
      </div>
    </form>
  );
...
```

We can also apply some simple CSS so the button also appears different when disabled (this is not a CSS course):

```css
button:disabled,
button:disabled:hover,
button:disabled:active {
  background-color: #ccc;
  color: #777;
  border-color: #999;
  cursor: not-allowed;
}
```

It's a cool concept. The argument of restricting submission goes either way. Some people argue you should allow them to submit to get feedback on validity. 

So, why did we use the `useEffect` hook? We technically don't need to do that, and it adds additional component re-evaluation cycles, which is not advantageous. We can actually create a `formIsValid` _derived state_. 

```js
const SimpleInput = (props) => {
  const [enteredName, setEnteredName] = useState('');
  const [enteredNameTouched, setEnteredNameTouched] = useState(false);

  const enteredNameIsValid = enteredName.trim() !== '';
  const nameInputIsInvalid = !enteredNameIsValid && enteredNameTouched;

  let formIsValid = false;
  
  if (enteredNameIsValid){
    formIsValid = true;
  }
...
```

That's a bit slimmer and simpler. 

**Challenge**
Add a second input to the form to fetch email address of user. Get the value and validate whether it's an email. The form should only be submittable if the inputs are valid. 

I almost got it right. But the trick is to contain each input in it's own `<div/>` element. This allows you to apply the `input:focus` on the input element. Basically, I tried to put `<input/>` elements cascading, and then apply the `:focus` pseudo selector to the class, which didn't work. 

Everything else is just like copying what is there for the name, except applying additional email validation logic. 

```js
import React, { useState } from 'react';

const SimpleInput = (props) => {
  // Name Input
  const [enteredName, setEnteredName] = useState('');
  const [enteredNameTouched, setEnteredNameTouched] = useState(false);

  const enteredNameIsValid = enteredName.trim() !== '';
  const nameInputIsInvalid = !enteredNameIsValid && enteredNameTouched;

  // Email Input
  const [enteredEmail, setEnteredEmail] = useState('');
  const [enteredEmailTouched, setEnteredEmailTouched] = useState(false);

  const trimmedEmail = enteredEmail.trim()
  const enteredEmailIsValid = trimmedEmail.includes('@', 1) && trimmedEmail.includes('.', 2);
  const emailInputIsInvalid = !enteredEmailIsValid && enteredEmailTouched;

  let formIsValid = false;
  
  if (enteredNameIsValid && enteredEmailIsValid){
    formIsValid = true;
  }

  const nameInputChangeHandler = event => {
    setEnteredName(event.target.value);
  }

  const nameInputBlurHandler = event => {
    setEnteredNameTouched(true);
  }

  const emailInputChangeHandler = event => {
    setEnteredEmail(event.target.value);
  }

  const emailInputBlurHandler = event => {
    setEnteredEmailTouched(true);
  }

  const formSubmissionHandler = event => {
    event.preventDefault();

    setEnteredNameTouched(true);
    setEnteredEmailTouched(true);

    if (!enteredNameIsValid || !enteredEmailIsValid) {
      return;
    }
    console.log(enteredName);
    console.log(enteredEmail);
    setEnteredName('');
    setEnteredEmail('');
    setEnteredNameTouched(false);
    setEnteredEmailTouched(false);
  }

  const nameInputClasses = nameInputIsInvalid ? 'form-control invalid' : 'form-control';
  const emailInputClasses = emailInputIsInvalid ? 'form-control invalid' : 'form-control';

  return (
    <form onSubmit={formSubmissionHandler}>
      <div className={nameInputClasses}>
        <label htmlFor='name'>Your Name</label>
        <input type='text' id='name' onChange={nameInputChangeHandler} onBlur={nameInputBlurHandler} value={enteredName}/>
        {nameInputIsInvalid && <p className='error-text'>Name must not be empty.</p>}
      </div>
      <div className={emailInputClasses}>
        <label htmlFor='email'>Your Email</label>
        <input type='email' id='email' onChange={emailInputChangeHandler} onBlur={emailInputBlurHandler} value={enteredEmail}/>
        {emailInputIsInvalid && <p className='error-text'>Email must contain "@" and "."</p>}
      </div>
      <div className="form-actions">
        <button disabled={!formIsValid}>Submit</button>
      </div>
    </form>
  );
};

export default SimpleInput;
```

You also need to adjust the form handler. It's a beefy component. You'd want to probably abstract some logic into another component or use a reducer or something. 

### Lesson 206: Adding a Custom Input Hook

We aren't duplicating the same words, but the logic is the same between the input elements. Image adding another `<input/>` element, it would be quite messy. So, we want to outsource some of the logic. 

One idea is to create a separate `<Input/>` component. The only "tricky" bit is managing the overall form validity. This would most likely involve passing state around between components. 

Another approach is to use a custom hook! It's more advanced, but also a bit more elegant in handling state. Start by adding `/app/src/hooks/use-input.js`. Of course, the file name in arbitrary, but this is suggested. Then, in the file, import React, create the component template, and export default. 

In the hook, we want to manage state. But we want it to be flexible, being able to accept the validation logic as a callback. In the custom hook, start by creating the states for the entered value, and the element being touched. Then we create inferred state. 

```js
import React, { useState } from "react";

const useInput = (validateValue) => {
    const [enteredValue, setEnteredValue] = useState('');
    const [isTouched, setIsTouched] = useState(false);

    const valueIsValid = validateValue(enteredValue);
    const hasError = !valueIsValid && isTouched;

    const valueChangeHandler = (event) => {
        setEnteredValue(event.target.value);
    }

    const valueInputBlurHandler = (event) => {
        setIsTouched(true);
    }

	const reset = () => {
		setEnteredValue('');
		setIsTouched(false);
	}

    return {
        value: enteredValue,
        isValid: valueIsValid,
        hasError,
        valueChangeHandler,
        valueInputBlurHandler,
        reset
    }
};

export default useInput;
```

In the above code example, you can see we accept a function into the hook's parameters to implement validation. We also even create event handler functions that interact with the hook's state, and return them in the object.  It's class. We return the parts that are needed in the parent component. We also create a handy `reset` method that can be called after the form is submitted. 

> If anything seems off about the writing, the course was going back and forth between components instead of writing them all at once. 

Now, back to the `<SimpleInput/>` component, we can import our custom hook and use it! Like any function, we can destructure the object returned to use throughout the component. We also need to create the validation function and pass that into the hook. Since our validation is simple, we can just create an anonymous inline function within the arguments of calling the custom hook. 

```js
import React, { useState } from 'react';
import useInput from '../hooks/use-input';

const SimpleInput = (props) => {
  const { 
    value: enteredName, 
    isValid: enteredNameIsValid,
    hasError: nameInputHasError, 
    valueChangeHandler: nameInputChangeHandler, 
    valueInputBlurHandler: nameInputBlurHandler,
    reset: resetNameInput
  } = useInput(value => value.trim() !== ''); 

  // Email Input
  const [enteredEmail, setEnteredEmail] = useState('');
  const [enteredEmailTouched, setEnteredEmailTouched] = useState(false);

  const trimmedEmail = enteredEmail.trim()
  const enteredEmailIsValid = trimmedEmail.includes('@', 1) && trimmedEmail.includes('.', 2);
  const emailInputIsInvalid = !enteredEmailIsValid && enteredEmailTouched;

  let formIsValid = false;

  if (enteredNameIsValid && enteredEmailIsValid) {
    formIsValid = true;
  }

  const emailInputChangeHandler = event => {
    setEnteredEmail(event.target.value);
  }

  const emailInputBlurHandler = event => {
    setEnteredEmailTouched(true);
  }

  const formSubmissionHandler = event => {
    event.preventDefault();

    setEnteredEmailTouched(true);

    if (!enteredNameIsValid || !enteredEmailIsValid) {
      return;
    }
    console.log(enteredName);
    console.log(enteredEmail);
    resetNameInput();
    setEnteredEmail('');
    setEnteredEmailTouched(false);
  }

  const nameInputClasses = nameInputHasError ? 'form-control invalid' : 'form-control';
  const emailInputClasses = emailInputIsInvalid ? 'form-control invalid' : 'form-control';

  return (
    <form onSubmit={formSubmissionHandler}>
      <div className={nameInputClasses}>
        <label htmlFor='name'>Your Name</label>
        <input type='text' id='name' onChange={nameInputChangeHandler} onBlur={nameInputBlurHandler} value={enteredName} />
        {nameInputHasError && <p className='error-text'>Name must not be empty.</p>}
      </div>
      <div className={emailInputClasses}>
        <label htmlFor='email'>Your Email</label>
        <input type='email' id='email' onChange={emailInputChangeHandler} onBlur={emailInputBlurHandler} value={enteredEmail} />
        {emailInputIsInvalid && <p className='error-text'>Email must contain "@" and "."</p>}
      </div>
      <div className="form-actions">
        <button disabled={!formIsValid}>Submit</button>
      </div>
    </form>
  );
};

export default SimpleInput;

```

Since we have the custom hook, we can remove creating state inside the component. We can also remove the functions to set state since it's in the custom hooks. If you changed any names when destructuring, ensure they are correct when called. We can swap out the `isInvalid` with the `hasError`, again, just additional confusion. 

We also have to go in to the `formSubmissionHandler` and change where it alters state. We will also call the `reset` method, which we aliased to `resetNameHandler()` to make more specific. 

Currently, we only changed the name input and left the email input alone. If the changes are actually implemented correctly, you won't have to make any changes to the JSX. Now, let's use our new custom hook to reduce the email input logic.

### Lesson 207: Re-Using the Custom Hook

Using the custom hook for the email. Just like the name value. After all of the updates, we actually can remove the `useState` import because all of the state is handled in the custom hook. 

```js
import React from 'react';
import useInput from '../hooks/use-input';

const SimpleInput = (props) => {
  const { 
    value: enteredName, 
    isValid: enteredNameIsValid,
    hasError: nameInputHasError, 
    valueChangeHandler: nameInputChangeHandler, 
    valueInputBlurHandler: nameInputBlurHandler,
    reset: resetNameInput
  } = useInput(value => value.trim() !== ''); 

  const { 
    value: enteredEmail, 
    isValid: enteredEmailIsValid,
    hasError: emailInputHasError, 
    valueChangeHandler: emailInputChangeHandler, 
    valueInputBlurHandler: emailInputBlurHandler,
    reset: resetEmailInput
  } = useInput(value => value.includes("@", 1) && value.includes('.', 2)); 

  let formIsValid = false;

  if (enteredNameIsValid && enteredEmailIsValid) {
    formIsValid = true;
  }

  const formSubmissionHandler = event => {
    event.preventDefault();

    setEnteredEmailTouched(true);

    if (!enteredNameIsValid || !enteredEmailIsValid) {
      return;
    }
    console.log(enteredName);
    console.log(enteredEmail);
    resetNameInput();
    resetEmailInput();
  }

  const nameInputClasses = nameInputHasError ? 'form-control invalid' : 'form-control';
  const emailInputClasses = emailInputHasError ? 'form-control invalid' : 'form-control';

  return (
    <form onSubmit={formSubmissionHandler}>
      <div className={nameInputClasses}>
        <label htmlFor='name'>Your Name</label>
        <input type='text' id='name' onChange={nameInputChangeHandler} onBlur={nameInputBlurHandler} value={enteredName} />
        {nameInputHasError && <p className='error-text'>Name must not be empty.</p>}
      </div>
      <div className={emailInputClasses}>
        <label htmlFor='email'>Your Email</label>
        <input type='email' id='email' onChange={emailInputChangeHandler} onBlur={emailInputBlurHandler} value={enteredEmail} />
        {emailInputHasError && <p className='error-text'>Email must contain "@" and "."</p>}
      </div>
      <div className="form-actions">
        <button disabled={!formIsValid}>Submit</button>
      </div>
    </form>
  );
};

export default SimpleInput;
```

### Lesson 208: A Challenge for you

We are now going to work with the `<BasicForm/>` component, which means swapping it in, in the `<App/>` component. 

This is the `<BasicForm/>` in its current state:

```js
import React from "react";

const BasicForm = (props) => {
  return (
    <form>
      <div className='control-group'>
        <div className='form-control'>
          <label htmlFor='name'>First Name</label>
          <input type='text' id='name' />
        </div>
        <div className='form-control'>
          <label htmlFor='name'>Last Name</label>
          <input type='text' id='name' />
        </div>
      </div>
      <div className='form-control'>
        <label htmlFor='name'>E-Mail Address</label>
        <input type='text' id='name' />
      </div>
      <div className='form-actions'>
        <button>Submit</button>
      </div>
    </form>
  );
};

export default BasicForm;
```

It has 3 inputs, is all JSX, and has no validation currently. It's a good time to try building the custom hook yourself and putting it into this component. 

### Lesson 209: Applying Custom Hooks to a New Form. 

This lesson will not build up the hook again. Any questions, please refer to the notes in the previous lessons. 

The lesson just covers how to use the custom hook again in a new form. Good to see such reusable code. Basically, once we have to custom hook, we instantiate its values, and then bind them to the JSX. Other things to do are to add styling by adding or removing CSS classes based on validity, add error messages, and disable the submit button. To disable the "submit" button, we need the overall form validity. 

Also, don't forget about the form submission handler! You need to `submitEvent.preventDefault();` so the page won't refresh. 

```js
import React from "react";
import useInput from "../hooks/use-input";

const isNotEmpty = value => value.trim() !== '';
const isEmail = value => value.trim().includes('@');

const BasicForm = (props) => {
  const {
    value: firstNameValue,
    isValid: firstNameIsValid,
    hasError: firstNameHasError,
    valueChangeHandler: firstNameChangeHandler,
    inputBlurHandler: firstNameBlurHandler,
    reset: resetFirstName,
  } = useInput(isNotEmpty);
  const {
    value: lastNameValue,
    isValid: lastNameIsValid,
    hasError: lastNameHasError,
    valueChangeHandler: lastNameChangeHandler,
    inputBlurHandler: lastNameBlurHandler,
    reset: resetLastName,
  } = useInput(isNotEmpty);
  const {
    value: emailValue,
    isValid: emailIsValid,
    hasError: emailHasError,
    valueChangeHandler: emailChangeHandler,
    inputBlurHandler: emailBlurHandler,
    reset: resetEmail,
  } = useInput(isEmail);

  const firstNameClass = firstNameHasError ? 'form-control invalid' : 'form-control';
  const lastNameClass = lastNameHasError ? 'form-control invalid' : 'form-control';
  const emailClass = emailHasError ? 'form-control invalid' : 'form-control';

  let formIsValid = false;

  if (firstNameIsValid && lastNameIsValid && emailIsValid) {
    formIsValid = true;
  }

  const submitHandler = event => {
    event.preventDefault();

    if (!formIsValid) {
      // user shouldn't get this far w/disabled submit button anyway. 
      return;
    }
    console.log("Submitted");
    console.log(firstNameValue, lastNameValue, emailValue);
    resetFirstName();
    resetLastName();
    resetEmail();
  }

  return (
    <form onSubmit={submitHandler}>
      <div className='control-group'>
        <div className={firstNameClass}>
          <label htmlFor='name'>First Name</label>
          <input type='text' id='name' value={firstNameValue} onChange={firstNameChangeHandler} onBlur={firstNameBlurHandler}/>
          {firstNameHasError && <p className="error-text">Please enter a first name.</p>}
        </div>
        <div className={lastNameClass}>
          <label htmlFor='name'>Last Name</label>
          <input type='text' id='name' value={lastNameValue} onChange={lastNameChangeHandler} onBlur={lastNameBlurHandler}/>
          {lastNameHasError && <p className="error-text">Please enter a last name.</p>}
        </div>
      </div>
      <div className={emailClass}>
        <label htmlFor='name'>E-Mail Address</label>
        <input type='text' id='name' value={emailValue} onChange={emailChangeHandler} onBlur={emailBlurHandler}/>
        {emailHasError && <p className="error-text">Please enter a valid email address.</p>}
      </div>
      <div className='form-actions'>
        <button disabled={!formIsValid}>Submit</button>
      </div>
    </form>
  );
};

export default BasicForm;
```

That is a lot to look over, but is just an example from all we have covered so far. 

### Lesson 210: Summary

[Creating a Custom useForm Hook](https://academind.com/tutorials/reactjs-a-custom-useform-hook) is a lengthy article about creating a custom hook to validate form inputs. It also returns input elements that you can put into your JSX, making it easy to integrate and reuse in a project. 

There are also 3rd party libraries, one such library being [formik](https://formik.org/), "build forms in React, without the tears." It uses more components and patterns instead of custom hooks. 

### Lesson 211: Bonus - Using useReducer()

We learned that using the `useReducer` hook is good if you need more state management power, have related pieces of state/data, or have more complex state updates, which probably constitutes needing more power. 

In our example, we don't really have a good example of needing the `useReducer` hook. However, it could be good practice to include it in our custom hook.

```JS
import { useReducer } from 'react';

const initialInputState = {
	value: '',
	isTouched: false
}

const inputStateReducer = (state, action) => {
	if (action.type === 'INPUT'){
		return {
			...state,
			value: action.value,
		}
	}
	...
	return initialInputState;
}

const useInput = (validateValue) => {
	const [inputState, dispatch] = useReducer(inputStateReducer, initialInputState);
	...
}
```

Above is the beginning to get started. You must import the hook and then create the "reducer function", which takes in a state snapshot and an action. We also typically create an initial state object, which I believe helps to setup the reducer in VS code. The `useReducer` itself will take in the reducer function and the initial state, and return the state and a dispatch function. 

When calling the dispatch function, we typically pass in an object for the action which includes a type and a payload. 

The rest of the actions and integration can be an exercise. 

### Lesson 212: Module Resources

Nothing new

## Section 17: Practice Project - Adding HTTP & Forms to the food order app

### Lesson 213: Module Introduction

We are looking to apply what we learned. We will want to add a checkout form, submit that data to a server / backend, we want to validate information, and we need to fetch meals data. 

The plan is to use Firebase again for the backend. And for the rules, you'll want the "read" and "write" set to true. 

### Lesson 214: Moving "Meals" data to the Backend

Literally just putting data into Firebase, almost like a JSON format. 

### Lesson 215: Fetching Meals via HTTP

One idea is to create a custom hook that utilizes the `fetch()` function, or utilize a 3rd party package. If you are writing your own, you'll probably want to use the `useEffect()` hook. 

Remember that `fetch()` returns a promise. Either use the `then()` method or the `async` and `await` keywords. If going the latter route, we don't want the actual function passed into `useEffect` to be asynchronous because of its return being a clean up. If you make it async, it will return a promise, which cannot be a clean up function. Instead, you can create another asynchronous function inside the `useEffect` hook, and call it. Basically, create and execute an IIFy. 

You can create and handle loading and error states for the data. 

### Lesson 216: Handling the Loading State

We might want to show error and loading states. Since we have many states, it might be handy to use the `useReducer` hook. 

One consideration is when do we set the `isLoading` state to true? You can initially set it to false, and then set it to true inside of the `useEffect` hook, but then that will trigger another iteration of loading components. If we intend loading to happen instantly, we can set the state to true from the start. 

However, if the component doesn't initiate loading by mounting, you might wait for an event, like submitting information, to initiate a loading state. Don't forget to set loading to false in the end.

### Lesson 217: Handling Errors

We should also handle errors. For example, if you fetch something and run into an error, you might get stuck on the loading screen. More of a UI theory concept, but it's a bad user experience because they wouldn't know what happened. 

You can have a generic "error" state, or you can make specific states for specific errors. Or better yet, `useReducer` can be used for more complex states. 

I do like how JavaScript has an `response.ok` boolean property that we can check. However, it may tell us the response is okay even if the status code is 404 or something.

```js
	useEffect(() => {
		const fetchData = async () => {
			const response = await fetch('https://getdata.com/api/');

			if (!response.ok){
				throw new Error('Something Went Wrong!');
			}
		}
	})
```

An advantage is that we can catch this error if something goes wrong with a `try-catch` block. That can be where you set "loading" to false, and our "error" to true. You can extract the `error.message` from our error object if you want to grab what we throw. 

The code above actually has a huge problem though, and that is the async function returns a promise. The try-catch block will therefore see a promise instead of an error. The "promise way" of handling errors is to use the `promise.catch((error)=> {})` method.

```js
...
	fetchData().catch(error => {
		setIsLoading(false);
		setHttpError(error.message);
	});
...
```

### Lesson 218: Adding A Checkout Form

Clicking the order button should expand the modal to a form for entering information. 

### Lesson 219: Reading Form Values

Adding some styling, a scrollable form in a modal. 

We can then use the `useRef` hook to get values from the form. Remember that you setup a ref by invoking it. Then, you use the special `<input ref={refName} />` "ref" prop to sync/link the ref to a component. And when you need the value stored in your "ref", you access the `refName.current.value` property. 

### Lesson 220: Adding Form Validation

You're validation logic can be more in-depth, but we will check values are not empty. Then we check if the form is valid or not as a whole. 

You'll see how cumbersome working with input-is-valid and input-is-touched states can be when working with large forms. It is a lot of state to manage in one component, arguably not best practices. 

The instructor likes to use inline ternary operators for setting CSS classes. 

### Lesson 221: Submitting and Sending Cart Data

For this example, we kind of have two forms, one with the user information and the other with their order/cart. That means we need to pass the user data to the cart component, and then send the complete request from there. 

Note: on the server, we shouldn't trust data you get from a client. There's an [Academind.com](https://academind.com/tutorials/hide-javascript-code) article, which I think was mentioned previously, which covers how JavaScript code is not hidden from the user. That means they can manipulate your validation be sending to the server. 

Always validation information on the server as well as on the front-end. However, this is a front-end course, so we will leave it there. 

### Lesson 222: Adding Better User Feedback

Just updating user feedback and such. We can create JSX variables outside of the return statement, and then use ternary operations to conditionally render JSX based on state. 

And since the cart stores orders in context, we need to create an action in the context to clear the cart. 

### Lesson 223: Summary

This section was just updating the food order app for practice. 

### Lesson 224: Module Resources

Ok

## Section 18: Diving into Redux (An Alternative to the Context API)

### Lesson 225: Module Introduction

We have covered enough to now dive into the very popular 3rd party library called **Redux**, which is used for managing app-wide state like context. We will discuss what is Redux and why would we need to use it. Then, we can diver into the basics and using it with React. And then, we can look at **Redux Toolkit**, which simplifies working with Redux. 