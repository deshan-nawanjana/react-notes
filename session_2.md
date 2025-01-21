# React Fundamentals

- [Elements Rendering](#elements-rendering)
- [Components and Props](#components-and-props)
- [Conditional Rendering](#conditional-rendering)
- [React Hooks](#react-hooks)
  - useState 📚 [docs](https://www.w3schools.com/react/react_usestate.asp)
  - useEffect 📚 [docs](https://www.w3schools.com/react/react_useeffect.asp)
  - useRef 📚 [docs](https://www.w3schools.com/react/react_useref.asp)

## Elements Rendering

Elements usually returns with one `parent element`.

```jsx
// function that returns elements
const App() {
  // return elements structure
  return (
    <div>
      <h1>
        Hello World
      </h1>
      <p>
        This is a paragraph
      </p>
    </div>
  )
}
```

Elements can be returned same as `variables` or `constants`.

```jsx
// function that returns elements
const App() {
  // define element
  const element = <h2>Hello</h2>
  // return element
  return element
}
```

Multiple elements with no parent should be an `array` or use
an `empty element`.

```jsx
// function that returns elements
const App() {
  // define elements
  const e_1 = <h2>Hello</h2>
  const e_2 = <h2>World</h2>
  // return both elements one after another
  return [e_1, e_1]
}
```

```jsx
// function that returns elements
const App() {
  // return two elements one after another
  return (
    <>
      <h2>Hello</h2>
      <h2>World</h2>
    </>
  )
}
```

Data in array can be arranged as list of elements.
`key` attribute is required when creating array of elements.
It should be unique to each element and cannot be repeated.
Therefore, `index of current item` is suitable for most of the time.

```jsx
// function that returns elements
const App() {
  // define data array
  const array = ["cat", "dog", "elephant", "deer"]
  // define output elements array
  const elements = []
  // for each item in data array
  for(let i = 0; i < array.length; i++) {
    // push a new button element with label
    elements.push(
      <button key={i}>
        {array[i]}
      </button>
    )
  }
  // return elements
  return (
    <div>
      <h3>
        Animals
      </h3>
      {elements}
    </div>
  )
}
```

Array mapping is much easier to generate list of elements.

```jsx
// function that returns elements
const App() {
  // define data array
  const array = ["cat", "dog", "elephant", "deer"]
  // return elements
  return (
    <div>
      <h3>
        Animals
      </h3>
      {
        array.map((item, index) => (
          <button key={index}>
            {item}
          </button>
        ))
      }
    </div>
  )
}
```

Element function may have constants, relative functions or any other
calculations before returning element.

```jsx
// element function
function App() {
  // define a function belongs to App
  function myFunction() {
    alert("You click me!")
  }
  // return elements with a button to trigger
  return (
    <div>
      <button onClick={myFunction}>
        Click This
      </button>
    </div>
  )
}


```

## Components and Props

Components are defined separately and can be reused.
Name of a component should always start with a `capital letter`.

```jsx
// child component
function MyComponent() {
  return (
    <div>
      Sample Text
    </div>
  )
}

// main component to reuse child component
function App() {
  return (
    <div>
      <h2>
        Reusing Components
      </h2>
      <MyComponent />
      <MyComponent />
    </div>
  )
}

```

Custom props can be passed into components as `attributes`.

```jsx
// child component with props
function MyComponent(props) {
  return (
    <div>
      <h1>
        Name: {props.name}
      </h1>
      <p>
        Age: {props.age}
      </p>
    </div>
  )
}

// main component to reuse child component
function App() {
  return (
    <div>
      <MyComponent name="John" age={32} />
      <MyComponent name="Jack" age={18} />
    </div>
  )
}

```

Props data type even can be a `function`.

```jsx
// child component with props
function MyComponent(props) {
  return (
    <div>
      <h1>
        Name: {props.name}
      </h1>
      <button onClick={() => props.selectItem(props.id)}>
        Select
      </button>
    </div>
  )
}

// main component to reuse child component
function App() {
  // function to select
  function select(id) {
    alert("You selected", id)
  }
  return (
    <div>
      <MyComponent id={10} name="John" selectItem={select} />
      <MyComponent id={15} name="Jack" selectItem={select} />
    </div>
  )
}

```

## Conditional Rendering

Rendering elements or components can be selected from `boolean expressions`.

```jsx
// function that returns elements
const App() {
  // define elements
  const element_1 = <h2>Hello</h2>
  const element_2 = <h2>World</h2>
  // conditional statement
  if (1 === 2) {
    return element_1
  } else {
    return element_2
  }
}
```

`Inline if statements` can make it more simple.

```jsx
// function that returns elements
const App() {
  // select elements by boolean statements
  return 1 === 2
    ? <h2>Hello</h2>
    : <h2>World</h2>
}
```

Child elements can be conditionally rendered using `curly brackets`.
Selection can be done through following methods:
- Pre-defined constant (with null)
- Inline if statement (with null)
- Boolean AND operator

```jsx
// function that returns elements
const App() {
  // pre-defined constant
  const child = 1 === 2
    ? <h2>World</h2>
    : null
  // return parent elements
  return (
    <div>
      <h1>Hello</h1>
      {child}
    </div>
  )
}
```

```jsx
// function that returns elements
const App() {
  // return parent elements with inline if statement
  return (
    <div>
      <h1>Hello</h1>
      {
        1 === 2
          ? <h2>World</h2>
          : null
      }
    </div>
  )
}
```

```jsx
// function that returns elements
const App() {
  // return parent elements with and operator
  return (
    <div>
      <h1>Hello</h1>
      {(1 === 2) && <h2>World</h2>}
    </div>
  )
}
```

## React Hooks

`useState` can be used to store a data which can be used
to update a component (re-rendering).
- State value does not update when you call the setter function right away.
- It takes some times to re-render the elements hierarchy.
- You can identify the change of state using `useEffect`.

### useState

```jsx
function App() {
  // state hook to remember counter value
  const [counter, setCounter] = useState(0)
  // return elements
  return (
    <div>
      <h1>You clicked {counter} times!</h1>
      <button onClick={() => setCounter(counter + 1)}>
        Click Me
      </button>
    </div>
  )
}
```

There can be `multiple states` for a component.

```jsx
function App() {
  // state hook to remember counter value
  const [counter, setCounter] = useState(0)
  // state hook to remember clicked time
  const [time, setTime] = useState(0)
  // function to click
  function clickEvent() {
    // increase counter
    setCounter(counter + 1)
    // remember clicked time
    setTime(Date.now())
  }
  // return elements
  return (
    <div>
      <h1>You clicked {counter} times!</h1>
      <h3>Last clicked at: {time}</h3>
      <button onClick={clickEvent}>
        Click Me
      </button>
    </div>
  )
}
```

Input element values can be bind into states using `onChange` event.

```jsx
function App() {
  // state hooks for form data
  const [name, setName] = useState("")
  const [age, setAge] = useState(18)
  const [gender, setGender] = useState("male")
  const [registered, setRegistered] = useState(false)
  // return elements
  return (
    <form>
      <input
        type="text"
        value={name}
        onChange={event => setName(event.target.value)}
      />
      <input
        type="number"
        value={age}
        onChange={event => setAge(event.target.value)}
      />
      <select
        value={gender}
        onChange={event => setGender(event.target.value)}>
        <option value="male">Male</option>
        <option value="female">Female</option>
      </select>
      <label>
        <input
          type="checkbox"
          checked={registered}
          onChange={event => setRegistered(event.target.checked)}
        />
      </label>
    </form>
  )
}
```

### useEffect

`useEffect` can be used to identify when a state value has been changed.
- useEffect should be defined with a `callback function` and `dependency array`.
- callback function will be called when `any of value` in dependency array has changed.

```jsx
function App() {
  // state hook to remember counter value
  const [counter, setCounter] = useState(0)
  // effect hook to callback on value change
  useEffect(() => {
    console.log("You clicked the button!")
  }, [counter])
  // return elements
  return (
    <div>
      <h1>You clicked {counter} times!</h1>
      <button onClick={() => setCounter(counter + 1)}>
        Click Me
      </button>
    </div>
  )
}
```

useEffect with `empty dependency array` can be used as mounted callback.
  - Mounted can be called twice in development server due to React `StrictMode`.

```jsx
function App() {
  // state hook to remember counter value
  const [counter, setCounter] = useState(0)
  // effect hook when only component mounted time
  useEffect(() => {
    console.log("Component mounted!")
  }, [])
  // return elements
  return (
    <div>
      <h1>You clicked {counter} times!</h1>
      <button onClick={() => setCounter(counter + 1)}>
        Click Me
      </button>
    </div>
  )
}
```

`useRef` can be used to hold a value in memory which `no effect`
to update the elements hierarchy.

```jsx
function App() {
  // ref hook to remember counter value
  const counter = useRef(0)
  // function to click
  function clickEvent() {
    // increase counter
    counter.current += 1
    // log counter
    console.log("You clicked ", counter.current, "times")
  }
  // return elements
  return (
    <div>
      <button onClick={clickEvent}>
        Click Me
      </button>
    </div>
  )
}
```
