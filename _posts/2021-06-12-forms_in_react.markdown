---
layout: post
title:      "Forms in React"
date:       2021-06-13 02:44:35 +0000
permalink:  forms_in_react
---


Forms are very important in react they allow our application to accept user input, whether it's logging in or creating or editing information.

#### Controlled vs Uncontrolled Input
There are two ways of handle input in React and that is either through controlled or uncontrolled inputs. 

##### Controlled
A controlled input is controlled by React and its value is set via a props. If you want to have a value, React wants that value to be coming from the state. To keep track of this value we need an onChange function that  keep track of every input change the user makes. To be able to use the same callback funtion in all input fields we should keep it dry and utilize the name attribute to grab that value. With controlled components we are also able to provide validations before the user submits the form.


first set state, which is where the value of our input will be living
```
state= {
        content: ""
}
```

then set up the function that will be updating the state when any changes happen and.
```
handleOnChange = event => this.setState({[event.target.name]: event.target.value})
```

In your input field
```
<input name="content" value={this.state.content} onChange={this.handleChange}/>
```

lastly we must provide an `onSubmit` callback fuction to our form.

#### uncontrolled

With an uncontrolled component we cannot invoke any validations until the form has been submitted since it is not tracking the iputs state like a controlled component would. It also does not exist in our virtual DOM(we are relying on the regular DOM), if you want to have value use defaultValue. Uncontrolled components are useful when dealing with file inputs or  using other libraries that do not interact with or follow Reacts design patterm.(there are many more reasons)
