# React v1.16 features
## Hooks Overview:
https://www.youtube.com/watch?v=dpw9EHDh2bM
 - useState hook in functional component
 - useContext hook in functional component
 - useEffect hook
 - custom hook (starting from use)

# Overview
https://www.educative.io/courses/reintroducing-react-v16-beyond
### Lifecycle
 - Mounting
 - Updating
 - Unmounting
 - Error handling

 getDerivedStateFromProps - not clear
 getSnapshotBeforeUpdate + componentDidUpdate - update DOM based on values. Scrolling to the latest item example.
 getDerivedStateFromError - no side effect
 componentDidCatch - side effect (like send error to the server)
 https://reactjs.org/docs/react-component.html

### Context API
```
import {createContext} from 'react';
const BennyPositionContext = createContext({ x: 50, y: 50 })
const { Provider, Consumer } = BennyPositionContext
```
Then provider is used in:
```
<Provider>
   // the root component for the Benny app. 
   <Benny /> 
</Provider>
```
And consumer
```
const Benny = () => {
  return <Consumer>
  	{(position) => <svg />}
	</Consumer>
}
```
https://react-hooks-cheatsheet.com/usecontext

### React.memo
Memoization of the pure component
```
mport React, { memo } from 'react'
export default  memo (function MyComponent (props) {  
    return ( <div>
        Hello World from {props.name.surname.short}       
     </div>
    )
}, equalityCheck)
function equalityCheck(prevProps, nextProps) {
  // return perform equality check & return true || false
} 
```

### Lazy loading (only JS)
Dynamic module loading:
```
import('path-to-awesome-module').then(module => {
     // do something with the module here e.g. module.default() to invoke the default export of the module.
 })
```
And in react:
```
// before 
import Scene from './Scene'
// now 
const Scene = React.lazy(() => import('./Scene'))
```
And also meanwhile show loading screen:
```
<Suspense fallback="<div>loading ...</div>">
  <Scene />
</Suspense>
```
### Profiler
https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en

### Hooks
https://react-hooks-cheatsheet.com/examples/fetching-data
*UseEffect*
```
useEffect(() => {
    console.log("useEffect first timer here.")
}, [count]) 
```
Second arguments is an array.
If it's empty, useEffect only called on the mount. If it contains objects, only on the update of these objects function is called.


# Advanced patterns
https://www.educative.io/courses/advanced-react-patterns-with-hooks
## Compound Components
```
import React, { createContext, useState, useCallback, useRef, useEffect, useMemo } from 'react'

const ExpandableContext = createContext()
const { Provider } = ExpandableContext

const Expandable = ({ children, onExpand }) => {
  const [expanded, setExpanded] = useState(false)
  const toggle = useCallback(
    () => setExpanded(prevExpanded => !prevExpanded),
    []
  )
  const componentJustMounted = useRef(true)
  useEffect(
    () => {
    if (!componentJustMounted.current) {
        onExpand(expanded)
      }
     componentJustMounted.current = false
    },
    [expanded]
  )
  const value = useMemo(
   () => ({ expanded, toggle }), 
   [expanded, toggle]
  )
  return (
    <Provider value={value}>
        {children}
    </Provider>
  )
}

export default Expandable
```