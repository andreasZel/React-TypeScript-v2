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
