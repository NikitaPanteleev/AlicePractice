# React TS.
https://www.youtube.com/watch?v=owcuEwn-pSM
http://slides.com/kamranayub/mjs-react-ts#/18
# Code organization
## absolute path
Ts aliases (ts config with compiler Options paths):
```
import NameSpace form 'src/NameSpace/`
```

## code organization
structure:
```
- features
-- actions.ts
-- reducers.ts
-- selectors.ts
-- service.ts
-- components
```

## array storage:
``
export interface NumericStoreState<T> {
  allIds: number[],
  byId: {[key: number]: T}
}
``