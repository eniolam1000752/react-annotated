﻿# **react-annotated**
A simple '@' annotation prefixed single line comment that cuts down time wasted on unnecessary instantiation or setting of react's state ( writing less coding more ).

#### native react's way

    /* react state declaration */
    const [count, setCount] = React.useState(0);
	
	/* variable usage and setter */
	const component = () => (
		<div onClick = { () => setCount(count + 1) }>
			Counting Number: {count}
		</div>
	)
#### react-annotated's way

    /* react state declaration */
    
    //@state
    let __count = 0;
	
	/* variable usage */
	const component = () => (
		<div onClick = { function (){ ++__count} }>
			Counting Number: { __count }
		</div>
	)
## Behind the hood
react-annotated is a babel plugin providing transformation of annotated declarations to it's equivalent native react transform on build time, resulting to zero latency effect at run-time.
#### transformation

    //@state
    let __variable = 'a word'

	/* transforms to */
	const [__variable, _SET__variable] = React.useState('a word');

 
    

## Installation

    npm install --save-dev react-annotated

## Available annotations

 - @state (ready for testing)
 - @consumer (in dev)
 - @provider (in dev)
 - @init (in dev)

## Usage
Note: react-annotated works for only functional react not classes.
#### Creating a react state
Declaring a react state is as simple as declaring a javascript variable though it's requires the following;

 - A single line comment annotation with the @ prefix at the top of the declaration.
 - A double underscore for variable name.

##### single state declaration
    //@state
    let __varable = 0;
##### multiple state declaration
    //@state
    let __varable = 0, 
	    __variable2 = 'string', 
	    __variable 3 = {}, 
	    __varaible4 = [];

#### Using a react state

    //@state
    let __variable = 0;
    
	const component = (props) => {
		return <div>{ __variable } </div>
	}
	
	/* output */
	<div> 0 </div>


#### Setting a react state
Setting a react's state is simply assigning a new value to the declared variable just as a usual javascript variable.
This can either be

 - An update expression
 - A single assignment expression
 - A nested assignment expression
   
##### Update Expression

	//@state
    let __variable = 0;
 
    const component = (props) => (
		<div onClick = { function (){ ++__variable} }>
			Counting Number: { __variable }
		</div>
	)

##### Assignment Expression

	//@state
    let __variable = 0;
 
    const component = (props) => (
		<div onClick = { () => { __variable = 'new value as string'} }>
			Counting Number: { __variable }
		</div>
	)
##### Nested assignment Expression

	//@state
    let __variable = 0, __variable2 = 3;
    let nonState = 5;
 
    const component = (props) => (
		<div onClick = { () => { __variable = __variable2 = ++nonState} }>
			Counting Number: { __variable }
		</div>
	)

#### Dependencies

 - [@babel/types](https://github.com/babel/babel/tree/master/packages/babel-types/src/definitions)
 - [@babel/template](https://github.com/babel/babel/tree/master/packages/babel-template)