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
