---
layout: post
title:      "Working with React Hooks"
date:       2020-07-17 00:40:40 +0000
permalink:  working_with_react_hooks
---


During my Flatiron journey, I was taught mostly class components and stateless functional components, which is very useful since a lot of legacy code, libraries, etc are written using classes and hooks have been around only for less than 3 years.

Class components are a good way to have an organized code, but as the logic of your component grows, everything starts to become messy and that's when React hooks come to the rescue.

Here's what a controlled form that takes a username and password looks like in a class component

```
class LoginForm extends React.Component {
	state = {
		username: "",
		password: ""
	}
	
	handleChange = e => {
	 this.setState({[e.target.name]:e.target.value})
	}
	
	handleSubmit = e => {
	 e.preventDefault()
	 this.setState({[e.target.name]:e.target.value})
	}

	render() {
	  const { username, password } = this.state
		return (
			<form onSubmit={this.handleSubmit}>
				<input type={"text"} name={"username"} value={username} onChange={this.handleChange} />
				<input type={"password"} name={"password"} value={password} onChange={this.handleChange} />
				<input type={"submit"} />
			</form>
		)
	}
}

```

So far it looks good and clean, but what if the page starts growing or what if more forms are needed? Are we gonna duplicate the same code that does the exact same work? No! Let's separate our logic from the component using hooks.

```
 const LoginForm = (props) => {
 
 // We hook to React's useState function directly and add a inital state just like in the class component
	const [state, setState] = useState({username: "", password: ""}) 
	const { username, password } = state // Destructure the state
	
	// Now we call the function that was returned from the useState hook. Notice how we don't need the word "this." anymore
	const handleChange = e => {
	 setState({[e.target.name]:e.target.value}) 
	}
	
	const handleSubmit = e => {
	//Here we need to copy the state, since useState hook doesn't merge the state as class components do
	 e.preventDefault()
	 setState({...state, [e.target.name]:e.target.value}) 
	}
	 
	return (
			<form onSubmit={handleSubmit}>
				<input type={"text"} name={"username"} value={username} onChange={handleChange} />
				<input type={"password"} name={"password"} value={password} onChange={handleChange} />
				<input type={"submit"} />
			</form>
		)
	
}
```

As you can see, we use the same structure of a stateless component and are now able to control our form with a bit less of code.

Notice how the useState hook was destructured: **const [state, setState] = useState({username: "", password: ""}) ** and how the inital state was passed.

Of course, we could also have define username and password independently:

```
 const [username, setUsername] = useState("")
 const [password, setPassword] = useState("")
 //We don't need to destructure the state anymore, as each input have their own variables assigned
```

It works the same, and it's a good pattern if you don't need to define a lot of variables, but else, stick with objects.

Even after using hooks, the component still looks too long for just rendering a basic form, but luckily we can create our own hooks to separate the logic from the rendering.

To create a custom hook, it needs to have the word "use" before the name of the component so that React recognizes it as a hook. Check [React's hooks rules](https://reactjs.org/docs/hooks-rules.html#:~:text=Only%20Call%20Hooks%20at%20the%20Top%20Level&text=Instead%2C%20always%20use%20Hooks%20at,multiple%20useState%20and%20useEffect%20calls.) for more information.

We are now creating a custom hook called useForm:

```
 const useForm = (initialState) => { // Just an arrow function that takes the initialState
 // The same logic we had, except we don't need to destructure anything yet
  const [state, setState] = useState(initialState) //Notice how you can call hooks inside of other hooks!
	
	const handleChange = e => {
	 setState({[e.target.name]:e.target.value})
	
	const handleSubmit = e => {
	 e.preventDefault()
	 setState({...state, [e.target.name]:e.target.value}) 
	}
	
	return { state, handleChange, handleSubmit} // And of course, the hook needs to return something, in this case the state and the handlers
	 
 }

export default useForm
```

Now that we created our own custom hook we can consume it in our LoginForm Component:

```
 const LoginForm = (props) => {
 
  // We call our custom hook and pass the initial state
  const { state, handleChange, handleSubmit } = useForm({username:"",password:""}) 
	
	//Destructure our data from the state
	const { username, password } = state
	
	//return our same form
	return (
			<form onSubmit={handleSubmit}>
				<input type={"text"} name={"username"} value={username} onChange={handleChange} />
				<input type={"password"} name={"password"} value={password} onChange={handleChange} />
				<input type={"submit"} />
			</form>
		)
		
 }
```

See how shorter the LoginForm looks. Now if we wanted a new form that had 10 fields for example, we could simply call the useForm hook, pass the initial state and get the data from state, without needing to rewrite or copy anymore.

Of course, this is only a brief example of hooks and why I've rewritten almost all of my projects to hooks. It is not necessary to change your code using hooks, but if your application is growing or you want to use React Native and only change the views but not your logic, hooks is the way to go.

There are many more hooks like [useEffect](https://reactjs.org/docs/hooks-effect.html), which behave like componentDidMount() and componentDidUpdate() combined.

React documentation is very complete and even if it might take you a while to understand hooks, trust me, it will be totally worth it.
