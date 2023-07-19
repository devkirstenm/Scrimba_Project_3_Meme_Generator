# Build a meme generator
Now we will move onto learning about building interactive web apps.

This module covers:
- event listeners
- state
- conditional rendering
- forms 
- side effects

## Event Listeners
```js
// Format
onClick
// Example:
import React from "react"

export default function App() {
    function handleClick() {
        console.log("I was clicked!")
    }
    return (
        <div className="container">
            <img src="https://picsum.photos/640/360" />
            <button onClick={handleClick}>Click me</button> {/* here */}
        </div>
    )
}
// Console: "I was clicked!"
```

Check this link for more event listeners:
https://legacy.reactjs.org/docs/events.html#mouse-events

### Let's revise! .map & event listeners
Go over this lesson again: https://scrimba.com/learn/learnreact/our-current-conundrum-co53a4b68be61be4a8e646607
```js

function App() {
    const thingsArray = ["Thing 1", "Thing 2"] 
    // .map
    const thingsElements = thingsArray.map(thing => <p key={thing}>{thing}</p>) // added key because it came up with a warning in the console to put this 
    
    // function that runs when button is click
    function addItem() {
        const newThingText = `Thing ${thingsArray.length + 1}`
        thingsArray.push(newThingText)
        console.log(thingsArray)
    }
    
    return (
        <div>
            {/*event listener*/}
            <button onClick={addItem}>Add Item</button>
            {thingsElements}
        </div>
    )
}
```


## State
When you type the above, the console won't change. This is because the following line (taken from the code above) only runs once (therefore only display thing 1, thing 2)

```js
   const thingsArray = ["Thing 1", "Thing 2"] 
    const thingsElements = thingsArray.map(thing => <p key={thing}>{thing}</p>)
```

### Props vs state props
Props - are data that a component receives from above and that shouldn't be changed

State - refers to value that are defined within a component and should be changing

### Quiz time! props vs state
1. How would you describe the concept of "state"?
State in a general sense means "the way things currently are."
In React, state refers to values that a component can maintain between render cycles. It's a way for React to remember saved values from within a component.
This is similar to declaring variables from within a component, with a few added bonuses (which we'll get to later)

2. When would you want to use props instead of state?
Anytime you want to pass data into a component so that
component can determine what will get displayed on the
screen.

3. When would you want to use state instead of props?
Anytime you want a component to maintain some values from
within the component. (And "remember" those values even
when React re-renders the component)

4. What does "immutable" mean? Are props immutable? Is state immutable?
Props are immutable, meaning "unchanging". We should never change props from the component receiving props.

State is mutable, you do plan on changing state, unlike props.

### useState
How to declare state :
```js
export default function App() {
    React.useState() // declaring useState (also written as useState() if declared in import like 'import React, {useState} from "react"')
    return ()}

// console displays:
[undefined, ƒ()] // we get an array back: first value is undefined, second value is a function

// what if we put string 'Hello'?
const result = React.useState("Hello")
    console.log(result) // displays '["Hello", ƒ()]'
```

### array destructuring
```js
// we can destructure the array and console.log what item you want in the array
   const [whateverWeWant, func] = React.useState("Yes") 
    console.log(result)
```

### useState practice: Counter app
```js
export default function App() {
    const [count, setCount] = React.useState(0)
    
    function add() {
        setCount(count + 1)
    }
    
    function subtract() {
        setCount(count - 1)
    }
    
    return (
        <div className="counter">
            <button className="counter--minus" onClick={subtract}>–</button>
            <div className="counter--count">
                <h1>{count}</h1>
            </div>
            <button className="counter--plus" onClick={add}>+</button>
        </div>
    )
} 
```

### Changing state with a callback function
```js
export default function App() {
    const [count, setCount] = React.useState(0)
    /**
     * Note: if you ever need the old value of state
     * to help you determine the new value of state,
     * you should pass a callback function to your
     * state setter function instead of using
     * state directly. This callback function will
     * receive the old value of state as its parameter,
     * which you can then use to determine your new
     * value of state.
     */
    function add() {
        setCount(prevCount => prevCount + 1) // using prev Count, return preCount + 1
    }
    // Challenge: update `substract` to use a callback function
    
    function subtract() {
        setCount(prevCount => prevCount - 1)
    }
    
    return ()}// return the rest
```

### Changing State Quiz!
1. You have 2 options for what you can pass in to a
   state setter function (e.g. `setCount`). What are they?
      
a. New value of state (setCount(42))
b. Callback function - whatever the callback function 
   returns === new value of state

2. When would you want to pass the first option (from answer
   above) to the state setter function?

Whenever you don't need the previous value of state to determine what the new value of state should be.

3. When would you want to pass the second option (from answer
   above) to the state setter function?

Whenever you DO need the previous value to determine the new value

### Ternary Operator Practice
Let's revise the ternary operator! Remember they allow us to put an if/else statement on a single line.
```js
/**
 * Challenge: Replace the if/else below with a ternary
 * to determine the text that should display on the page
 */

    // original code
    const isGoingOut = true
    
    let answer  // Use ternary here
    if(isGoingOut === true) {
        answer = "Yes"
    } else {
        answer = "No"
    }   

// ANSWER:
// you can write it either way:
// a) option a 
 const isGoingOut = true
    // here we set out answer equal to: then use a ternary to determine if isGoingOut is true. If it is, set the answer to yes, otherwise no
    let answer = isGoingOut === true ? "Yes" : "No"

// b) option b
  const isGoingOut = false
    let answer = isGoingOut === true ? "Yes" : "No"
    

// c) simpler way
    const isGoingOut = false
    // isGoingOut was already set to false therefore you don't need to repeat it
    let answer = isGoingOut ? "Yes" : "No"
```

### Flipping state back & forth - complex example incorporating state & ternary operator 
```js
import React from "react"

export default function App() {
    // 1. Initialize state for `isGoingOut` as a boolean
    const [isGoingOut, setIsGoingOut] = React.useState(true)
    
    /**
     * Challenge: 
     * - 1. Initialize state for `isGoingOut` as a boolean
     * - 2. Make it so clicking the div.state--value flips that
     *   boolean value (true -> false, false -> true)
     * - 3. Display "Yes" if `isGoingOut` is `true`, "No" otherwise
     */

    // 2. Make it so clicking the div.state--value flips that
     *   boolean value (true -> false, false -> true)
    function changeMind() {
        // with setIsGoingOut, take previous state and return opposite of what prevState used to be
        setIsGoingOut(prevState => !prevState) // same as writing 'prevState ? false : true'
    }
    
    return (
        <div className="state">
            <h1 className="state--title">Do I feel like going out tonight?</h1>
            <div onClick={changeMind} className="state--value">
                {/* 3. Display "Yes" if `isGoingOut` is `true`, "No" otherwise */}
                <h1>{isGoingOut ? "Yes" : "No"}</h1>
            </div>
        </div>
    )
}
```
### Complex state: arrays
Convert the code to use an array held in state
```js
function App() {
    /**
     * Challenge: Convert the code below to use an array
     * held in state instead of a local variable. Initialize 
     * the state array with the same 2 items below
     * 
     * Don't worry about fixing `addItem` quite yet.
     */
    const thingsArray = ["Thing 1", "Thing 2"]
}

// ANSWER
    const [thingsArray, setThingsArray] = React.useState(["Thing 1", "Thing 2"])
```

Make it so that the 'add item' button will add things to the array
```js
function App() {
    // define state
    const [thingsArray, setThingsArray] = React.useState(["Thing 1", "Thing 2"])
    
    function addItem() {
        // modify state (setThingsArray) & provide callback function to change state
        setThingsArray(prevState => {
            //  & return a new state '=> []': prevState SO FAR & the prevState + 1
            return [...prevState, `Thing, ${prevState.length + 1}`]
        })
    }
    
    const thingsElements = thingsArray.map(thing => <p key={thing}>{thing}</p>)
    
    return (
        <div>
            {/* when button is clicked, run the addItem function */}
            <button onClick={addItem}>Add Item</button>
            {/* & then display thingsElements */}
            {thingsElements}
        </div>
    )
}
```

### Complex state: objects
When we click the favorite (star) button, it must change to favorite/unfavorite.
```js
export default function App() {
    const [contact, setContact] = React.useState({
        firstName: "John",
        lastName: "Doe",
        phone: "+1 (719) 555-1212",
        email: "itsmyrealname@example.com",
        isFavorite: true
    })
        })
    /**
     * Challenge: Use a ternary to determine which star image filename
     * should be used based on the `contact.isFavorite` property
     * 
     * `true` => "star-filled.png"
     * `false` => "star-empty.png"
     * 
     */
    let starIcon = contact.isFavorite ? "star-filled.png" : "star-empty.png"
    
    function toggleFavorite() {
        console.log("Toggle Favorite")
    }
    
     /**
     * Challenge: Fill in the values in the markup
     * using the properties of our state object above
     * (Ignore `isFavorite` for now)
     */
    return (
        <main>
            <article className="card">
                <img src="./images/user.png" className="card--image" />
                <div className="card--info">
                    <img 
                        {/* Then use the starIcon value to display the correct image */}
                        src={`../images/${starIcon}`} 
                        className="card--favorite"
                        onClick={toggleFavorite}
                    />
                    <h2 className="card--name">
                        {contact.firstName} {contact.lastName}
                    </h2>
                    <p className="card--contact">{contact.phone}</p>
                    <p className="card--contact">{contact.email}</p>
                </div>
                
            </article>
        </main>
    )
```

### Complex state: updating state objects
When we click the star icon, we want it to flip the 'isFavorite' property so that it can be favorited/unfavorited.
```js
    let starIcon = contact.isFavorite ? "star-filled.png" : "star-empty.png"
    
    function toggleFavorite() {
        // given our previous contact, i want to return an object that has all of the values of our prevContact but changes the isFavorite value to be opposite of what it currently is
        setContact(prevContact => {
            return {
                // // This:
                        // firstName: "John",
                        // lastName: "Doe",
                        // phone: "+1 (719) 555-1212",
                        // email: "itsmyrealname@example.com",
                        // isFavorite: true,  
                ...prevContact, //is the same as this. You do this so that all the information (name, phone etc. stays on the card when you favorite/unfavorite, otherwise it would only display the star)
                isFavorite: !prevContact.isFavorite
            }
        })
    }
```

### Refactor state for our project
```js
export default function Meme() {
/**
 * Challenge: Update our state to save the meme-related
 * data as an object called `meme`. It should have the
 * following 3 properties:
 * topText, bottomText, randomImage.
 * 
 * The 2 text states can default to empty strings for now,
 * amd randomImage should default to "http://i.imgflip.com/1bij.jpg"
 * 
 * Next, create a new state variable called `allMemeImages`
 * which will default to `memesData`, which we imported above
 * 
 * Lastly, update the `getMemeImage` function and the markup 
 * to reflect our newly reformed state object and array in the
 * correct way.
 */

    // state variable
    const [meme, setMeme] = React.useState({
        topText: "",
        bottomText: "",
        randomImage: "http://i.imgflip.com/1bij.jpg" 
    })
   
    // another state variable
    const [allMemeImages, setAllMemeImages] = React.useState(memesData)    
    
    function getMemeImage() {
        // anywhere we were accessing memesData, we now use allMemeImages
        const memesArray = allMemeImages.data.memes
        const randomNumber = Math.floor(Math.random() * memesArray.length)
        const url = memesArray[randomNumber].url
        setMeme(prevMeme => ({
            ...prevMeme,
            randomImage: url
        }))
        
    }
    
    return (
        <main>
            <div className="form">
                <input 
                    type="text"
                    placeholder="Top text"
                    className="form--input"
                />
                <input 
                    type="text"
                    placeholder="Bottom text"
                    className="form--input"
                />
                <button 
                    className="form--button"
                    onClick={getMemeImage}
                >
                    Get a new meme image 🖼
                </button>
            </div>
            <img src={meme.randomImage} className="meme--image" />
        </main>
    )
}
```

## Styling in React
```js
import React from "react"
import boxes from "./boxes"

export default function App(props) {
    const [squares, setSquares] = React.useState(boxes)
    
    const styles = {
        backgroundColor: props.darkMode ? "#222222" : "#cccccc"
    }
    
    const squareElements = squares.map(square => (
        <div style={styles} className="box" key={square.id}></div>
    ))
    return (
        <main>
            {squareElements}
        </main>
    )
}
```

## Conditional Rendering

### Conditional rending: &&
We learned already about how the && operator is used to make sure that both sides are true.
```js
    const cond1 = true
    const cond2 = true
    if(cond1 && cond2) { // If both true...
        // ...this code will run 
    // if either is false, this code will NOT run
    }
```
IMPORTANT NOTE: The computer first checks the truthiness of the first statement, the 'cond1', and if it is not truthy (it's falsy), it completely skips whatever is after the '&&'. This is because it already knows, if the first statement is false, that this does not meet the condition of the "&&" operator.

This is important in conditional rendering, because we can take whatever we want to show/hide as the second statement, to only display if the first statement is true. We wouldn't want to show it (put it as the first statement) first.
```js
export default function Joke(props) {
    const [isShown, setIsShown] = React.useState(false)

    function toggleShown(){
        setIsShown(prevShown => !prevShown)
    }
    return (
        <div>
            {props.setup && <h3>{props.setup}</h3>}
            {/**
            * Challenge:
            * - Only display the punchline paragraph if `isShown` is true
            */}
            {isShown && <p>{props.punchline}</p>} {/* if isShown is true and this paragraph after, then only will the p tag display*/}
            <button onClick={toggleShown}>Show Punchline</button>
            <hr />
        </div>
    )
}
```

### Conditional rendering: && practice
```js

export default function App() {
    const [messages, setMessages] = React.useState(["a", "b"]) // there are is 2 messages
    /**
     * Challenge:
     * - Only display the <h1> below if there are unread messages
     */
    return (
        <div>
            {messages.length > 0
            &&
            <h1>You have {messages.length} unread messages!</h1>}
        </div>
    )
}
// console displays: You have 2 unread messages!
```

### Conditional rendering: ternary
```js
export default function Joke(props) {
    const [isShown, setIsShown] = React.useState(false)
    function toggleShown(){
        setIsShown(prevShown => !prevShown)
    }
    return (
        <div>
            <h3>{props.setup}</h3> {/* show props.setup from jokesData.js*/}
            {isShown && <p>{props.punchline}</p>} {/* only show punchline if isShown is true */}
            <button onClick={toggleShown}>{isShown ? "Hide This" : "Show This"} Punchline</button> /{/* if isShown is true = show button with text that says "Hide", other "Show"*/}
            <hr />
        </div>
    )
```

### Conditional rendering practice
```js
export default function App() {
    const [messages, setMessages] = React.useState(["a"])
    /**
     * Challenge:
     * - If there are no unread messages, display "You're all caught up!"
     * - If there are > 0 unread messages, display "You have <n> unread
     *   message(s)"
     *      - If there's exactly 1 unread message, it should read "message"
     *        (singular)
     */
    return (
        <div>
            {
                messages.length === 0 ? // if messages.length is 0, display...
                <h1>You're all caught up!</h1> : // ... this, otherwise display...
                <h1>You have {messages.length} unread  {messages.length > 1 ? "messages" : "message"}</h1> // ...this (note ? messages : message has to do with showing message(s) depending on how many messages there are)
            }
        </div>
    )
}
```

### Conditional rendering quiz!
1. What is "conditional rendering"?
- When we want to only sometimes display something on the page
based on a condition of some sort


2. When would you use &&?
- When you want to either display something or NOT display it


3. When would you use a ternary?
- When you need to decide which thing among 2 options to display


4. What if you need to decide between > 2 options on
   what to display?
- Use an `if...else if... else` conditional or a `switch` statement
 
## Forms: simple example
Here's a simple example where a user types their name into a form input.
The state will update with every key input
```js
export default function Form() {
    // 1. we need state to hold the current data that's typed into our input (an empty string)
    const [firstName, setFirstName] = React.useState("")

    console.log(firstName) // fires every time you type into input box (so you can see the letters you are typing are working)
    // 2. 
    function handleChange(event) { // event object is passed to browser
        setFirstName(event.target.value) // don't need to know what state used to be, to determine what state is going to be, because we have easy access to the information put into the input box by accessing 'event.target.value'
    }

    return (
        <form>
            <input
                type="text"
                placeholder="First Name"
                // 2. listen for any changes that happen to the input
                onChange={handleChange}
            />
        </form>
    )
}
```

### Forms: more complex example (when we have multiple inputs)
- Here we combine our state (first & last name) into an object.
- And how to use the event parameter that we receive in our function event handler to determine which property of that state object we should be updating

```js
export default function Form() {
    // initial state
    const [formData, setFormData] = React.useState(
        {firstName: "", lastName: ""} // an empty first and last name will show as initial state
    )

     console.log(formData) // console logging it so we can observe the state each time it changes
    
    function handleChange(event) {
        // because we have multiple properties, we do now use prevData. WHY? Imagine we have lots of other properties that we need to maintain (keep their data) and not overwrite.
        setFormData(prevFormData => {
            return {
                ...prevFormData, // keep old object intact
                // we only need to overwrite specific properties
                [event.target.name]: event.target.value // key: value pairs. '[event.target.name]' key turns this string to use it as a property name for our object
            }
        })
    }

    return (
        <form>
            <input
                type="text"
                placeholder="First Name"
                onChange={handleChange}
                name="firstName" // NB: name property must match name in state property
            />
            <input
                type="text"
                placeholder="Last Name"
                onChange={handleChange}
                name="lastName"
            />
        </form>
    )
}

/* console display:
* {firstName: "asdfg", lastName: "qwert"}
*/
```

### Forms: controlled inputs
```js
    return (
        <form>
            <input
                type="text"
                placeholder="First Name"
                onChange={handleChange}
                name="firstName"
                // add value property to each input
                // add piece of state into value property
                value={formData.firstName}
            />
    )
```
Visually there's no change. Conceptually however, when you type into the first name, the value of this input box is no longer being controlled by the input, but by React.

This is important because if you don't do this React sometimes complains about "uncontrolled components".


### Forms: Textarea
```js
/**
 * Challenge: Add a textarea for "comments" to the form
 * Make sure to update state when it changes.
 */

// 1. add comments to state
    const [formData, setFormData] = React.useState(
        {firstName: "", lastName: "", email: "", comments: ""}
    )

// 2. add a textarea for comments to form
<textarea 
    // no need to add type as its already suggested in its name "textarea"
    value={formData.comments}
    placeholder="Comments"
    onChange={handleChange}
    name="comments"
/>
```

### Forms: Checkbox
```js
export default function Form() {
    const [formData, setFormData] = React.useState(
        {
            firstName: "", 
            lastName: "", 
            email: "", 
            comments: "", 
            // Checkboxes are either true or false
            isFriendly: true // as default (true) this is checked already
        }
    )
    
    function handleChange(event) {
        const {name, value, type, checked} = event.target
        setFormData(prevFormData => {
            return {
                ...prevFormData,
                [name]: type === "checkbox" ? checked : value // if type is equal to checkbox, use the checked property, otherwise use the value property. When you're setting your FormData, it must use the type: checked for the Checkbox (it's value is currently true^), but for the others (email, comments etc.) it must use their values
            }
        })
    }
    
    return (
        <form>
            {/* other form elements omitted for readability sake */} 
            <input 
                type="checkbox" 
                id="isFriendly" 
                checked={formData.isFriendly}
                onChange={handleChange}
                name="isFriendly" // must match what's in state
            />
            <label htmlFor="isFriendly">Are you friendly?</label>
            <br />
        </form>
    )
}

```

### Forms: Radio Buttons
Radio buttons have some kind text value to them (unemployed, part-time etc.).

When a user clicks one of these options ^, 
we will be watching for changes in these inputs,
and when a change happens... it will take the value of *that* radio button that was clicked and set our state [employment: ""] to that value.
```js
export default function Form() {
    const [formData, setFormData] = React.useState(
        {
            firstName: "", 
            lastName: "", 
            email: "", 
            comments: "", 
            isFriendly: true,
            employment: ""
        }
    )
    console.log(formData.employment)
    
    function handleChange(event) {
        const {name, value, type, checked} = event.target
        setFormData(prevFormData => {
            return {
                ...prevFormData,
                [name]: type === "checkbox" ? checked : value // checks if type is checkbox, see's it isn't (it's type is radio), so it then takes the value instead
            }
        })
    }
    
    return (
        <form>
            {/* other form elements omitted for readability sake */} 
            <fieldset>
                <legend>Current employment status</legend>
                
                <input 
                    type="radio"
                    id="unemployed"
                    name="employment"
                    value="unemployed" // the value that will get saved in state when this input is selected
                    checked={formData.employment === "unemployed"}
                    onChange={handleChange} // event listener
                />
                <label htmlFor="unemployed">Unemployed</label>
                <br />
                
                <input 
                    type="radio"
                    id="part-time"
                    name="employment"
                    value="part-time"
                    checked={formData.employment === "part-time"}
                    onChange={handleChange}
                />
                <label htmlFor="part-time">Part-time</label>
                <br />
                
                <input 
                    type="radio"
                    id="full-time"
                    name="employment"
                    value="full-time"
                    checked={formData.employment === "full-time"}
                    onChange={handleChange}
                />
                <label htmlFor="full-time">Full-time</label>
                <br />
                
            </fieldset>
        </form>
    )
}

```

### Forms: Select & Option
This is a select box that you can click on and it opens a number of options to choose from
```js
export default function Form() {
    const [formData, setFormData] = React.useState(
        {
            firstName: "", 
            lastName: "", 
            email: "", 
            comments: "", 
            isFriendly: true,
            employment: "",
            favColor: ""
        }
    )
    console.log(formData.favColor)
    
    function handleChange(event) {
        console.log(event)
        const {name, value, type, checked} = event.target
        setFormData(prevFormData => {
            return {
                ...prevFormData,
                [name]: type === "checkbox" ? checked : value
            }
        })
    }
    
    return (
        <form>
            {/* other form elements omitted for readability sake */} 
            <label htmlFor="favColor">What is your favorite color?</label>
            <br />
            <select 
                id="favColor"
                value={formData.favColor}
                onChange={handleChange}
                name="favColor"
            >
                <option value="">-- Choose --</option>
                <option value="red">Red</option>
                <option value="orange">Orange</option>
                <option value="yellow">Yellow</option>
                <option value="green">Green</option>
                <option value="blue">Blue</option>
                <option value="indigo">Indigo</option>
                <option value="violet">Violet</option>
            </select>
        </form>
    )
}
```

### Forms: Submitting a form

```js
export default function Form() {
    const [formData, setFormData] = React.useState(
        {
            firstName: "", 
            lastName: "", 
            email: "", 
            comments: "", 
            isFriendly: true,
            employment: "",
            favColor: ""
        }
    )
    
    function handleChange(event) {
        const {name, value, type, checked} = event.target
        setFormData(prevFormData => {
            return {
                ...prevFormData,
                [name]: type === "checkbox" ? checked : value
            }
        })
    }
    
    function handleSubmit(event) {
        event.preventDefault()
        // submitToApi(formData)
        console.log(formData)
    }
    
    return (
        <form onSubmit={handleSubmit}>
            {/* other form elements omitted for readability sake */} 
            <br />
            <br />
            {/* SUBMIT BUTTON:
            * Button is automatically set to "submit".
            * This is because the button is within the <form>, and will therefore automatically trigger the forms onSubmit event handler 'onSubmit={handleSubmit}'.*/}
            <button>Submit</button>
        </form>
    )
}

/** CONSOLE DISPLAYS:
 * ›{firstName: "Bob", lastName: "Ziroll", email: "", comments: "lsladkfjhasdf", isFriendly: true, employment: "full-time", favColor: "blue"}
 */
```

### Forms Quiz!
1. In a vanilla JS app, at what point in the form submission
   process do you gather all the data from the filled-out form?
   - In JS: Right before the form is submitted. You listen for the form submit event (e.g., button click to submit) and it'll go to each element in the form and gather the data.


2. In a React app, when do you gather all the data from
   the filled-out form?
   - In REACT: As the form is being filled out. The form element aren't allowed to maintain their own internal state, and instead the component that houses the entire form has some React state and that state is updated on every change from the elements in the form. (Remember when we logged this to the console, it displayed every single keystroke)


3. Which attribute in the form elements (value, name, onChange, etc.)
   should match the property name being held in state for that input?
   - `name` property should match. Remember we have 'name="employment" in our <form> and in the function 'const {name,...'
   


4. What's different about a saving the data from a checkbox element
   vs. other form elements?
    - A checkbox uses the `checked` property to determine what should be saved in state. Other form elements use the `value` property instead.


5. How do you watch for a form submit? How can you trigger
   a form submit?
    - Can watch for the submit with an onSubmit handler on the `form` element.
    - Can trigger the form submit with a button click.


### Forms practice
```js
    /**
     * Challenge: Connect the form to local state
     * 
     * 1. Create a state object to store the 4 values we need to save.
     * 2. Create a single handleChange function that can
     *    manage the state of all the inputs and set it up
     *    correctly
     * 3. When the user clicks "Sign up", check if the 
     *    password & confirmation match each other. If
     *    so, log "Successfully signed up" to the console.
     *    If not, log "passwords do not match" to the console.
     * 4. Also when submitting the form, if the person checked
     *    the "newsletter" checkbox, log "Thanks for signing
     *    up for our newsletter!" to the console.
     */

// 1. Create state object
export default function App() {
    const [formData, setFormData] = React.useState({
        email: "",
        password: "",
        passwordConfirm: "",
        joinedNewsletter: true // automatically checked
    })
    
    // 6. Create handleChange function
    function handleChange(event) {
        const {name, value, type, checked} = event.target
        setFormData(prevFormData => ({
            ...prevFormData,
            [name]: type === "checkbox" ? checked : value
        }))
    }
    
    function handleSubmit(event) {
        event.preventDefault()
        if(formData.password === formData.passwordConfirm) {
            console.log("Successfully signed up")
        } else {
            console.log("Passwords do not match")
            return // the if statement below (thanks for signing up) will not run unless the password situation is sorted out
        }
        
        if(formData.joinedNewsletter) {
            console.log("Thanks for signing up for our newsletter!")
        }
    }
    
    return (
        <div className="form-container">
            <form className="form" onSubmit={handleSubmit}>
                <input 
                    type="email" 
                    placeholder="Email address"
                    className="form--input"
                    // 2. Add these properties as a name field in each one of our inputs 
                    name="email"
                    // 3. Add an onChange event that'll point to your function (point 6)
                    onChange={handleChange}
                    // 5. Add a value property, so that their values can change. NOTE: checkbox will have 'checked' instead of value
                    value={formData.email}
                />
                <input 
                    type="password" 
                    placeholder="Password"
                    className="form--input"
                    name="password"
                    onChange={handleChange}
                    value={formData.password}
                />
                <input 
                    type="password" 
                    placeholder="Confirm password"
                    className="form--input"
                    name="passwordConfirm"
                    onChange={handleChange}
                    value={formData.passwordConfirm}
                />
                
                <div className="form--marketing">
                    <input
                        id="okayToEmail"
                        type="checkbox"
                        name="joinedNewsletter"
                        onChange={handleChange}
                        checked={formData.joinedNewsletter}
                    />
                    <label htmlFor="okayToEmail">I want to join the newsletter</label>
                </div>
                <button 
                    className="form--submit"
                >
                    Sign up
                </button>
            </form>
        </div>
    )
}

```

## Making API Calls
A very common thing you'll have to do in React is interact with an API that lives outside of your application.

Instead of having a folder that contains all your data (in this case all the meme images in the 'memesData.jsx' file), you can your data from an API.

Here's an example of a simple API that contains all the data needed: https://swapi.dev/api/people/1

Usually what you're doing is either:
* requesting info from an API
* submitting info to an API

GETTING DATA FROM AN API:
    1. Get the data (fetch)
    2. Save the data to state (so application can use it)

SYNTAX:  
```js
    fetch("https://swapi.dev/api/people/1") // fetch request to the Star Wars API
    .then(res => res.json())// fetch receives a response, which will be json, that we will turn into a js object that we can use
    .then(data => console.log(data)) // console log the data

/**
 * CONSOLE DISPLAYS this object:
 * {name: "Luke Skywalker", height: "172", mass: "77", hair_color: "blond", skin_color: "fair", ETC...}
 */
```

## Side Effects
WHAT IS A (OUT)SIDE EFFECT?
    Anything that lives outside Reacts reach, for example:
    * localStorage on your own browser
    * API/database interactions
    * Subscriptions (e.g., web sockets)
    * Syncing 2 different internal states together
    * Basically anything React isn't in charge of is a side effect

HOW TO MANAGE SIDE EFFECTS (re-render issue)
        Hook: 'useEffect()' 
    Tool that allows us to interact outside of the React ecosystem

```js
React.useEffect(function() { // can have 1 or 2 (optional) parameters
    fetch("https://swapi.dev/api/people/1") // put your side effect code here (stuff from outside)

        .then(res => res.json())
        .then(data => setStarWarsData(data))
}) 
```

### useEffect Quiz!
1. What is a "side effect" in React? What are some examples?
    - It's any code you want to run that React isn't in charge of handling, code that has an effect on some outside system (such as an API)


2. What is NOT a "side effect" in React? Examples?
    - Anything that React is in charge of.
    - Maintaining state, keeping the UI in sync with the data, render DOM elements


3. When does React run your useEffect function? When does it NOT run the effect function?
    - As soon as the component loads (first render)
    - On every re-render of the component (assuming no dependencies array)
    - Will NOT run the effect when the values of the dependencies in the array stay the same between renders
   


4. How would you explain what the "dependecies array" is?
    - Second paramter to the useEffect function
    - A way for React to know whether it should re-run the effect function


#### useEffect Challenge
```js

export default function App() {
    const [starWarsData, setStarWarsData] = React.useState({})
    const [count, setCount] = React.useState(1)
    
    /**
     1. Combine `count` with the request URL so pressing the "Get Next Character" button will get a new character from the Star Wars API.
     2. Remember: don't forget to consider the dependencies array!
     */
    
    React.useEffect(function() {
        console.log("Effect ran")
        // 1. ADD 'COUNT' TO URL
        fetch(`https://swapi.dev/api/people/${count}`)
            .then(res => res.json())
            .then(data => setStarWarsData(data))
        //2 . ADD COUNT TO DEPENDENCIES ARRAY
    }, [count]) // TRIGGERS THIS WHOLE FUNCTION AGAIN
    
    return (
        <div>
            <h2>The count is {count}</h2>
            <button onClick={() => setCount(prevCount => prevCount + 1)}>Get Next Character</button>
            <pre>{JSON.stringify(starWarsData, null, 2)}</pre>
        </div>
    )
}
```

### useEffect cleanup function
```js
export default function WindowTracker() {
    
    const [windowWidth, setWindowWidth] = React.useState(window.innerWidth)
    
    React.useEffect(() => {
        function watchWidth() {
            console.log("Setting up...")
            setWindowWidth(window.innerWidth)
        }
        
        window.addEventListener("resize", watchWidth)
        
        // CLEANUP FUNCTION
        return function() {
            console.log("Cleaning up...")
            window.removeEventListener ("resize", watchWidth) // so that it doesn't trigger this
        }
    }, [])
    
    return (
        <h1>Window width: {windowWidth}</h1>
    )
}
```
```js
 /**
    useEffect takes a function as its parameter. If that function
    returns something, it needs to be a cleanup function. Otherwise,
    it should return nothing. If we make it an async function, it
    automatically retuns a promise instead of a function or nothing.
    Therefore, if you want to use async operations inside of useEffect,
    you need to define the function separately inside of the callback
    function, as seen below:
    */
    
    React.useEffect(() => {
        async function getMemes() {
            const res = await fetch("https://api.imgflip.com/get_memes")
            const data = await res.json()
            setAllMemes(data.data.memes)
        }
        getMemes()
    }, [])
```