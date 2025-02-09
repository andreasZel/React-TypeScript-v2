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

const reducer = (state = initialState, action: { type: 'increment' | 'decrement' | 'reset' | 'updateByValue', payload?: number }) => {
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

# Utils

1. `miragejs` : simulates an API, so that we can make UI before the backend is ready
