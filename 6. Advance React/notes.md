Week 1:
	note:
		The map() method in JavaScript is used to transform lists of data.
		
		
	note:
		Traditional HTML forms keep some internal state inside the DOM and have some default behavior when submitting them.
		and that is done via the action attribute.
		
	Note: controlled component:
			this offers declarative api
			State delegation is performed via the value prop. A combination of local state and the value prop is needed to create a controlled component.
			
	Note: Props are a component's configuration, received from parents in the tree and are immutable.		
	
Week 2:
		Note:
			Pure function: 
				Are one which have no side effect.
				Return value does not depend on  any external paramenter.
				Always return same value no matter how many time you invoke that function.
			
			Impure functions: 
				Are one whcih have side effect.
				Return different value.
			
		Note:
			Main rules of using hooks:
				Only call hooks from a React component function.
				Only call hooks at the top level.
				We can call multiple state or effect hooks
				Make multiple hooks calls in the same sequence.
					If you’re making multiple hook calls, you always need to call them in the same sequence. You do have to always make multiple hook calls in the same sequence.
				
		Note: JavaScript is single threaded.
		
		Note:
			Fetch function is a way to call a browser Api from javascript.
		
		Note:
			Few things we look for and follow when we are desiging an API. 
				One of them is type safety. Type safety is when we are requesting an photo from an api, we need (should) get photo. not video or data or somethinng. 
		
		Note: useReducer:
			useState has one limitation i.e it is difficult to use useState when we have one state depend on other state. 
				So in that case we can use useReducer instead of useState.
				
			useState							
				starts with initial state 
				best used on less complex data while working with primitive data type (string, numbers, boolean)

			useReducer
				starts with initial state and reducer function
				best used on more complex data (like objects and arrays)
				
			Ex of useReducer:
			
				
				import {useReducer} from "react";
				
				// reducer function takes previous state (staate) and action as an input. It takes previous state and returns new state.
				const reducer = (staate, action) => {
					if(action.type === "buy") return {money: staate.money - 10};
					if(action.type === "sell") return {money: staate.money + 10};
					return staate;
				}
				
				
				function App() {
					const initialState = {money: 100};
					const [state, dispatch] = useReducer(reducer, initialState);
				
					return (
						<h1>Wallet Money: {state.money}</h1>
						<button onClick={() => dispatch({type: "buy"})}>Shopping </button>
						<button onClick={() => dispatch({type: "sell"})}>Sell Meal </button>
					);
				}
		
		Note: "proper way to handle console.log() invocations is to use the useEffect hook."
		
		Example for useRef:
		
			import {useRef} from "react";
			
			function App(){
			
				const inputFieldRef = useRef(null);
				
				const handleClick = () => {
					inputFieldRef.current.focus(); 			//here focus() is the plain javascript method for input field.
				}
				
				return (
					<input ref={inputFieldRef}  type="text" />
					<button onClick={handleClick}>Click to focus input field</button>
				);
			
			}
			
		Custom Hook:
			Minimum requirement of custom hook:
				The custom hook should use at least one built-in React hook.
				
				
Week 3:
		JSX : Syntax extension to JS
		
		each node is a plain js object discribing a DOM node
		
		jsx:
			<button className = "button">
				<span>Submit</span>
				<CustomComponent color="blue" />
			</button>
			
		jsx converted to Elements  (an intermidatory representation created by react):
			{
				type: "button",
				props: {
					className: "button"
					children: [
						{
							type: "span",
							children: "Submit"
						},
						{
							type: "CustomComponent",
							props: {
								color: "blue"
							}
						}
					]
				}
			}
			
		Two key features of component composition are Containment and Specialization
			
		Containment: It refers to the fact that some components don’t know their children ahead of time.
						And can also be described as generic boxes, like a Dialog or Alert.  
			
		Specialization: It defines components as being “special cases” of other components. 
							For example, the ConfirmationDialog is a special case of Dialog.
							
							
		Popular react API's:	React.cloneElement and React.children
		
			React.cloneElement:
				
				Use of React.cloneElement:
					Modify children properties.
					Add to children properties.
					Extend funcionality of children
				
				Syntax:
					React.cloneElement(element, [props])	//element ---> element which you like to clone ;  [props]  ---> will be added and merged into original props into the component.
			
			
			React.children: It provides utility.
				
				Syntax :
					React.Children.map(children, <tranformation_function_which_return_new_react_element>)
					
					
	Cross-cutting concerns:
		Permission roles, Handling errors, Logging, are some group of funcionality which falls under cross-cutting concerns.
		These above are not necessary from business point of view but evey application needs it.
		To implement this custom hooks may not be a best solution, so that where Higher order component (HOC) is used.
			A higher-order component also known as a HOC is an advanced pattern that emerges from React's compositional nature.
				HOC is a function takes a component and returns a new component.
				Whereas a component transforms props into UI, a higher-order components transforms a component into another component. In other words it enhances and extends the capabilility of a component.
				You can define logic in a single place, share it across many components, and keep them unchanged and stateless.

				Note: connect is a function that returns a higher-order component, presenting a valuable property for composing several HOCs together.
				Note: compose(f, g, h) is the same as (...args) => f(g(h(...args)))
				
				Note: The with part of the HOC name is a general convention recommended by React, as it expresses the enhancing nature of the technique, like providing a component ‘with’ something else.
				
			
			Note: there are several ways of code reusablity 1. using HOC  2. Using render props pattern
			
			Render props pattern:
				Takes function that return React element and call them inside their render logic.
				New props are injected dynamically as the parameter of the function.
				Note: The DataFetcher component returns the result of calling the render function and has no other rendering business.
				
	
	Intergrating test with react library:
		Best practice to follow:
			Avoid including implementation details.
			Work with DOM nodes
			More you test more Resemble software usage
			Maintainability for log run.
		
		2 popular testing tools:
		
			1. Jest: 
				It is a javascript test runner
				It lets you to access artificial DOM called jsdom
				It provide good iteration speed with powerful feaures like Mocking modules
			
			2. React testing library:
				It is set of utility
				Fulfils all best practice of testing.
					
			
		Note:
			Screen.getByLabelText asks the root document to find a label tag whose text contains a specified text value and then return the input element associated with that label.
		Note:
			To fill the input and update the state with a value, you can use the fireEvent.change() utility from React Testing Library. 
			
	Note:
		Some of the features of component containment:
			A component that acts as a generic box.
			A component that uses the children prop to pass children elements directly as their content.
			The fact that some components don’t know their children ahead of time.
			
		All components have by default have "children" prop
		
		What is a React Element?
			An intermediary representation that describes a component instance.
			A JavaScript object that represents the final HTML output.
			
		Usecase of React.cloneElement API:
			Extend the functionality of children components. 
			Modify children's properties. 
			Add to children properties.
		
		what are valid solutions to encapsulate cross-cutting concerns?
			Higher order components.
			Render props pattern. 
			Custom hooks.
			
		The screen utility object from react-testing-library represents the root document when performing queries against it.
		
		When writing tests with Jest and react-testing-library, you would use toHaveAttribute to assert that a button is disabled.
			

Week 4:
	Formik : Formik is another popular open-source library that helps you to create forms in React. The library takes care of the repetitive tasks of managing the state of the form, validation and submission, so you can focus on the business logic of your application. 
	
	Yup is a JavaScript open-source library used to validate the form data before submitting it to the server. It provides a set of chainable operators that you can apply to your form fields to declaratively specify the validation rules.
				
