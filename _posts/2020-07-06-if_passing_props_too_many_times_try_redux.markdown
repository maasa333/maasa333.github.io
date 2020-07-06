---
layout: post
title:      "If passing props too many times, try Redux"
date:       2020-07-06 22:13:09 +0000
permalink:  if_passing_props_too_many_times_try_redux
---


In my last post, I described how React components can pass `props` (properties) down from parent to child.  This works great and all, but what if you had a child component waaaaaaaaaaaaaaaaaay down the tree structure that only needed one prop from the top parent component?  In a normal React application, you would have to pass down that one single prop through all the components in between in order to give that bottom child component access to it.

While there is nothing particularly wrong with this, I think you might see how passing down props through many components can start to get a little messy.  There's more room for error, and when an error does come up, it might be more complicated to trace where the issue is coming from (assuming that it is one related to props). 


## Redux to the rescue!

Redux, a small library that complements React (and any other JavaScript framework or library), is a state management tool.  With Redux, you have something called the `store`, which is where your app's global state is held.  When a component has access to the Redux store, instead of waiting for props to get passed down from above, the component can grab whatever state properties it needs to use directly from the store!


## Example usage

Let's start out with a simple component called SomeComponent that is a class component:

*(Note:  Only a class component can access the Redux store, since it can hold its own state.)*

```
import React, { Component } from 'react';

class SomeComponent extends Component { 

  render() {
	  return (
		  <div>
		    {/*  We want to return the a prop from state here */}
			</div>
		);
	}
}

export default SomeComponent;
```

Assuming you have already set up Redux in your index.js file, make the following changes to this component in order to access the store:

```
import React, { Component } from 'react';
import { connect } from 'react-redux'

class SomeComponent extends Component { 

  render() {
	  return (
		  <div>
		    {/*  We want to return the a prop from state here */}
			</div>
		);
	}
	
	const mapStateToProps = state => {
	  return {
		  thingy: state.thingy
		}
	}
	
export default connect(mapStateToProps)(SomeComponent);
}
```

Here, we have imported `connect` from the react-redux library.  We have also wrapped the export default SomeComponent with `connect`, and passed in a function called `mapStateToProps`.  This function accepts `state` as an argument, and it will return whatever specific attribute/property of state you want for this component and make it available as a `prop`. 

What this now means, is that SomeComponent now has a prop of `thingy` that it can use here, and also pass down to the child component like you would do with any other prop.  

Let's finalize this component so that it will render the prop `thingy` that we just grabbed from the Redux store: 

```
import React, { Component } from 'react';
import { connect } from 'react-redux'

class SomeComponent extends Component { 

  render() {
	  return (
		  <div>
			  {this.props.thingy} 
			</div>
		);
	}
	
	const mapStateToProps = state => {
	  return {
		  thingy: state.thingy
		}
	}
	
export default connect(mapStateToProps)(SomeComponent);
}
```

And that's it!  From here on out, that prop can be treated just like regular props in React. 

Keep in mind that there is more to Redux!  This is just an example of how Redux can help save the time and energy of having to pass props down through several components, and it will also make debugging easier. 
