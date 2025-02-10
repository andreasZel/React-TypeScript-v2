# Type vs Interface

1. `Interface`
   it's like a class that you can extend and override individual
   properties

2. `Type`
   it is a little bit more constraint but can be extended. For example we
   can add optional or mandatory fields using `&` and `|`:

   ```Javascript
      type Person = {
         name: string;
         surname: string;
      }

      type InternalStudent = Person & { student_id: number }

      type ExternalStudent = InternalStudent & { external_university: string }

      type Student = InternalStudent | ExternalStudent
   ```

Generaly interface are good for libraries and external things, whereas
type more for internal

# Passing children as a prop

We can achieve this with either `ReactNode` or `PropsWithChildren<T>`
the benefit of `PropsWithChildren<T>` is that we can specify the props that are
passed with the children

if we want to pass children but also styles we sould define

```Javascript
   type propType =  PropsWithChildren<{
      style: CSSProperties
   }>
```

# Creating props for HTML exelents and extend them

there is a `ComponentPropsWithoutRef<T>` that can take T = 'button' or
any other element that gets all props for that element

# Typing Reducers

Reducers are function that get current state and next state and return a value. So a
simple way to define a reducer would be:

```Javascript
   const reducer = (count: number, newValue: number): number => {
      return newValue
   };

   const [count, setCount] = useReducer(reducer, 0);
```

Typically a reducer would contain a state and an action to follow, so in the same
manner:

```Javascript
type InitialState = {
  count: number;
};

const initialState: InitialState = {
  count: 0
};

type Action = {
  type: 'increment' | 'decrement' | 'reset'
};

type ActionWithPayload = {
  type: 'updateByValue',
  payload: number;
}

const reducer = (state = initialState, action: Action | ActionWithPayload) => {
  const { count } = state;

  if (action.type === 'increment') {
    const newCount = count + 1;
    return { count: newCount };
  }

  if (action.type === 'decrement') {
    const newCount = count - 1;
    return { count: newCount };
  }

  if (action.type === 'reset') {
    return { count: 0 };
  }

  if (action.type === 'updateByValue') {
    return { count: Number(action.payload) };
  }

  return state;
};

const [{ count }, dispatch] = useReducer(reducer, initialState);
```

We can redefine each types and define dispatch using the default import from react:

```Javascript
import { Dispatch } from 'react';

type adjustcountActions = Action | ActionWithPayload;

type AdjustColorsProps = {
  count: number;
  dipatch: Dispatch<adjustcountActions>
};
```

or we can create a **`global.d.ts`** that has all our types without export
and the IDE autoImports them!

# Template literals

We can use template literals to dynamically change types like:

```Javascript
 type HexColor = `#${string}`;

 // we can use the HexColor to check if a color is valid
 const isHexColor = (s: string): s is HexColor => {
   return s.startsWith('#');
 }

 type RGBString = `rgb(${number}, ${number}, ${number})`
```

or maybe generate action basef on formats:

```Javascript
 type ColorFormats = 'rgb' | 'hex' | 'hsl' | 'hsv';

 // this will have update-rgb-color, update-hex-color, ...
 type ActionTypes = `update-${ColorFormats}-color`

```

# Getting types from values

if we have an array value like:

```Javascript
  //readonly
  const status = ['loading', 'error', 'success'] as const;

  //this gives 'loading' | 'error' | 'success'
  type Statuses = (typeof status)[number];
```

# Omit and Partial

1. `Partial`: makes all of properties optional

2. `Omit`: reoves properties defined
   for example if we want to remove `id`:

   ```Javascript
    type Item = {
      id: string;
      name: string;
      packed: boolean;
    };

    type changedItems = Omit<Partial<Item>, 'id'>;
   ```

```

# Utils

1. `miragejs` : simulates an API, so that we can make UI before the backend is ready
```
