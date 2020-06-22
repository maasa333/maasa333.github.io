---
layout: post
title:      "Please Pass the Props"
date:       2020-06-22 07:39:59 +0000
permalink:  please_pass_the_props
---


It took me a bit to get comfortable with the usage of *props* in React/Redux, but after loads of practice and repetition, I feel that I have a much better grasp on it.

In React, *props* (short for *properties*) is an attribute of a React Component that can get passed down to other components.  Props can only be passed down from parent to child components, not the other way around (unless you use a function to pass props back up, but I won't be talking about that here). 

Let's say we have a bank that's loaded with cash (as they most often do), and I am requesting some to put into my wallet.  We will need to make a (parent) `BankComponent` and a (child) `WalletComponent`.  Now, to pass the (props) `cash` down, our `BankComponent` will first need to have access to it in its own props....  But where is the `cash` coming from?? 

In this case, we're going to connect the `BankComponent` to the Redux *store* (perhaps you can think of the store as the Federal Reserve Banks in this scenario), and use the `mapStateToProps` function to do just as the function says.  In this function, we are able to take a specific piece of state from the store and map it as props for our component.

The code version of the statement above is as follows:

```
import React, { Component } from 'react';
import { connect } from 'react-redux';

class BankComponent extends Component {
		 
  render() {
    return (
      <div>
        
      </div>
      )
    }
  }
 
 const mapStateToProps = state => {
   return { 
     cash:  state.cash 
    } 
 }
 
export default connect(mapStateToProps)(BankComponent);

```

Now, to pass the `cash` on down to our `WalletComponent`, the child component will need to be rendered as follows:

```
import React, { Component } from 'react';
import { connect } from 'react-redux';

// NEW CODE
import WalletComponent from './components/WalletComponent';

class BankComponent extends Component {
		 
  render() {
    return (
      <div>
        //NEW CODE
        <WalletComponent />
      </div>
      )
    }
  }

...
```

But just rendering the `WalletComponent` isn't enough!  It is at this point where we can now pass the `cash` (props) down, so our `WalletComponent` can have access to it.  To pass props down, pass it into the component like this: 

```
<WalletComponent money={this.props.cash} />
```

When it comes to the way the passed in props are named, the variable (`money` in our case) can be named anything, but just know that whatever variable name you give it here is how you will call it as a prop in the actual component.  Typically, the variable name would probably just have been `cash`, but I'm calling it `money` so it'll hopefully be a little clearer as to how it comes up as a prop in the child component. 

The value assigned (`{this.props.cash}`) is simply how the desired prop is accessed in the current component. 

Now that our `WalletComponent` has `cash`, this is what the component will look like: 

```
import React, { Component } from 'react';

class WalletComponent extends Component {
		 
  render() {
    return (
      <div>
        Here is the $$$: {this.props.money}
      </div>
      )
    }
  }
 
export default WalletComponent;
```

Notice that I'm calling `{this.props.money}` here as opposed to `{this.props.cash}`.  That is because when the prop was passed to the `WalletComponent`, the prop was given the variable name `money`.

I hope this helps!  React and Redux have been extremely tough, to say the least, and I never thought I'd understand any of it when starting out this module.  I promise you though, with continued practice and repetition, it will inevitably make more sense. 
