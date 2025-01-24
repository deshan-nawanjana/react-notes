# React Router (Declarative routing for React)

- React Router router can `conditionally render` components according to current `url pathname`.
- There are two main modes for the React Router
  - `BrowserRouter` - Works with regular url paths. (Ex: /about)
  - `HashRouter` - Works with hash paths. (Ex: /#/about)
- To use `BrowserRouter`, all the url requests should be pointed to the same index.html from the server side.
- `HashRouter` works with client side hash change. Therefore it does not require any server side support.

Creating the components (such as pages) to render according to the route.

```jsx
export default function Home() {
  return <div>This is Home</div>
}
```

```jsx
export default function Projects() {
  return <div>This is Projects</div>
}
```

```jsx
export default function About() {
  return <div>This is About</div>
}
```

While configuring the React Router, `<BrowserRouter>` should be a parent component wrapped around the entire application.
  - `<Routes>` can be used anywhere when you need to conditionally render set of components.
  - Set of `<Route>` components should be inside `<Routes>` with each rendering components with their pathname.

While navigating from below example, each component will be rendered as follows.
  - http://localhost:3000/ - `<Home />`
  - http://localhost:3000/about - `<About />`
  - http://localhost:3000/projects - `<Projects />`

```jsx
// import router components
import { BrowserRouter, Route, Routes } from "react-router-dom"
// import pages
import Home from "./pages/Home.jsx"
import About from "./pages/About.jsx"
import Projects from "./pages/Projects.jsx"

// configure browser router
createRoot(document.getElementById("root")).render(
  <StrictMode>
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/projects" element={<Projects />} />
      </Routes>
    </BrowserRouter>
  </StrictMode>
)
```

Same way `HashRouter` can be configured. Only requirement is to use `<HashRouter>` instead of `<BrowserRouter>`.

While navigating from below example, each component will be rendered as follows.
  - http://localhost:3000/#/ - `<Home />`
  - http://localhost:3000/#/about - `<About />`
  - http://localhost:3000/#/projects - `<Projects />`

```jsx
// import router components
import { HashRouter, Route, Routes } from "react-router-dom"
// import pages
import Home from "./pages/Home.jsx"
import About from "./pages/About.jsx"
import Projects from "./pages/Projects.jsx"

// configure browser router
createRoot(document.getElementById("root")).render(
  <StrictMode>
    <HashRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/projects" element={<Projects />} />
      </Routes>
    </HashRouter>
  </StrictMode>
)
```

`<Link>` component can be used as navigation controls. This component can navigate between paths without refreshing the page.

```jsx
// import router components
import { BrowserRouter, Route, Routes, Link } from "react-router-dom"
// import pages
import Home from "./pages/Home.jsx"
import About from "./pages/About.jsx"
import Projects from "./pages/Projects.jsx"

// configure browser router
createRoot(document.getElementById("root")).render(
  <StrictMode>
    <BrowserRouter>
      {/* navigation links */}
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
      <Link to="/projects">Projects</Link>
      {/* routes */}
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/projects" element={<Projects />} />
      </Routes>
    </BrowserRouter>
  </StrictMode>
)
```

`useNavigate` hook can be used to navigate from coding level instead of user actions such as link clicks.

```jsx
// import router components
import { Route, Routes, useNavigate } from "react-router-dom"
// import pages
import Home from "./pages/Home"
import About from "./pages/About"
import Projects from "./pages/Projects"

function App() {
  // create navigate hook
  const navigate = useNavigate()
  // some method will use navigation
  const onLogin = () => {
    navigate("/projects")
  }
  // component with routes
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<About />} />
      <Route path="/projects" element={<Projects />} />
    </Routes>
  )
}
```

# MUI (User Interface Library)

- 📚 [Components Library and Usage](https://mui.com/material-ui/all-components/)
- 📚 [Icons Library](https://mui.com/material-ui/material-icons/)

Install MUI packages into the project.

```bash
npm install @emotion/react @emotion/styled @mui/material @mui/icons-material
```

Instead of using regular JSX elements, MUI library components can be used.

```jsx
// import components and icons
import { Button, Input, Rating } from "@mui/material"
import { Home } from "@mui/icons-material"

function App() {
  return (
    <div>
      {/* input component */}
      <Input type="text" />
      {/* button component */}
      <Button variant="contained">
        Click Me
      </Button>
      {/* rating component */}
      <Rating />
      {/* home icon */}
      <Home />
      {/* button component string home icon */}
      <Button variant="contained" startIcon={<Home />}>
        Click Me
      </Button>
    </div>
  )
}
```