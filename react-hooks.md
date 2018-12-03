#### Hooks
* `useState`:
 
```js
  import React, {useState} from 'react'

  function Counter() {
    const [count, setCount] = useState(0)
    const increment = () => setCount(count + 1)
    return <button onClick={increment}>{count}</button>
  }

  export default Counter
```

* **Custom hook**
```js
import React, {useState} from 'react'

function useCounter({initialState, step}) {
  const [count, setCount] = useState(initialState)
  const increment = () => setCount(count + step)
  return {count, increment, setCount}
}

function Counter() {
  const {count, increment} = useCounter({initialState: 5, step: 3})
  return <button onClick={increment}>{count}</button>
}

export default Counter
```

* `useReducer`:


* `useContext`:


* `useEffect`:
