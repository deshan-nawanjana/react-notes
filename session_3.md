# Redux Toolkit (State Management + REST APIs Query)

- 📚 [State Management Docs](https://redux.js.org/usage/)
- 📚 [REST APIs Query Docs](https://redux-toolkit.js.org/tutorials/rtk-query)

- React built-in hook `useState` can store data that related to a `specific component`.
- Redux Toolkit can handle `global level` of states that can be access and changes from `anywhere` in the application.

Redux Toolkit can be installed into your project
using following command.

```bash
npm install @reduxjs/toolkit react-redux
```

### Redux State Management

- Redux Store is usually configured for an entire application.
- Slices are configured for each sector of the application.
  - Ex: loginSlice, homeSlice, settingsSlice.
  - Each slice will contain data related to that specific sector. 
- If the application is small, one slice is enough.
- All the slices will be connected to a store.

Creating slice with `initialState` data object and `reducers`.
  - `initialState` is the initial data structure.
  - `reducers` are methods to update that data structure.
  - `slice actions` should be exported to use in anywhere.

```js
// import methods from reduxjs library
import { createSlice } from "@reduxjs/toolkit"

// create a slice for the app
const slice = createSlice({
  // unique name for the slice
  name: "commonSlice",
  // initial data structure
  initialState: {
    name: "",
    email: "",
    age: 20
  },
  // data reducers
  reducers: {
    // to update each form item
    setName(state, action) {
      state.name = action.payload
    },
    setEmail(state, action) {
      state.email = action.payload
    },
    setAge(state, action) {
      state.age = action.payload
    },
    // to reset all form item
    resetForm(state) {
      state.name = ""
      state.email = ""
      state.age = 20
    }
  }
})

// export slice actions
export const {
  setName,
  setEmail,
  setAge,
  resetForm
} = slice.actions
```

Configuring the score and connect slice ot it.

```js
// configure store
const store = configureStore({
  reducer: {
    common: slice.reducer
  }
})

// export store
export { store }
```

Wrapping the root app component with store provider.

```js
// import redux provider
import { Provider } from "react-redux"
// import configured store
import { store } from "./path/to/store"

// wrap with provider
createRoot(document.getElementById('root')).render(
  <Provider store={store}>
    <App />
  </Provider>
)
```

Using `useSelector` redux hook it is possible to read the data
in the slice from anywhere in the application.

```jsx
// import redux hook
import { useSelector } from "react-redux"

// some component in the app
function App() {
  // get store values from common slice
  const name = useSelector(states => states.common.name)
  const email = useSelector(states => states.common.email)
  const age = useSelector(states => states.common.age)
  // return screen by code
  return (
    <form>
      <input type="text" value={name} />
      <input type="email" value={email} />
      <input type="number" value={age} />
    </form>
  )
}
```

Using `useDispatch` redux hook and slice action it is possible
to update a value in the store.

```jsx
// import redux hooks
import { useSelector, useDispatch } from "react-redux"
// import slice action
import { setName } from "./path/to/store"

// some component in the app
function App() {
  // dispatch hook
  const dispatch = useDispatch()
  // get store values from common slice
  const name = useSelector(states => states.common.name)
  // return screen by code
  return (
    <form>
      <input
        type="text"
        value={name}
        onChange={event => dispatch(setName(event.target.value))}
      />
    </form>
  )
}
```

### Redux Query for REST APIs

`createApi` method can configure a collection of REST API endpoints.

```js
// import method
import { createApi } from "@reduxjs/toolkit/query/react"

// configure endpoints collection
const commonAPI = createApi({
  reducerPath: "commonAPI"
  baseQuery: fetchBaseQuery({
    // api base url
    baseUrl: "https://sample.com/api"
  }),
  endpoints: builder => ({
    // login endpoint
    login: builder.mutation({
      query: ({ username, password }) => ({
        url: "/login",
        method: "POST",
        body: { username, password }
      })
    }),
    // logged user data endpoint
    getUserData: builder.mutation({
      query: () => ({
        url: "/user",
        method: "GET",
        headers: {
          Authorization: localStorage.getItem("token")
        }
      })
    })
  })
})

// export api endpoints
export const {
  useLoginMutation,
  useGetUserDataMutation
} = commonAPI

// export api
export default commonAPI
```
Binding the configured api into Redux store will enable
to use the API inside the application.

```js
// import configured api
import commonAPI from "./path/to/commonAPI"

// configure store
const store = configureStore({
  reducer: {
    // any slice reducers
    common: slice.reducer,
    // set api reducer
    [commonAPI.reducerPath]: commonAPI.reducer
  },
  middleware: getDefaultMiddleware => (
    getDefaultMiddleware()
      // concat api middleware
      .concat(commonAPI.middleware)
  )
})

// export store
export { store }
```

Usage of API endpoints

```jsx
// import api endpoints
import { useLoginMutation } from "./path/to/commonAPI"

// login component
function Login() {
  // create api hook
  const [login] = useLoginMutation()
  // form states
  const [username, setUsername] = useState("")
  const [password, setPassword] = useState("")
  // login method
  const onLogin = () => {
    // call the api with request body data
    getAffiliate({ username, password }).then(response => {
      // use logged data such as token
      console.log(response.data.token)
    })
  }
  // login form
  return (
    <div>
      <button onClick={onLogin}>
        Login
      </button>
    </div>
  )
}

```
