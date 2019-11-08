# The Structure of Intermediate Compilation Files

- Extension: `.remuic`
- Sketch: Providing the analysed information for a given record object(like a module in ML)
- File contents:
    - hash value of the contents
    - filename
    - type of the record
    - type definitions of the record
    - number of values
    - type of each value
    - information of available infix operators, mainly about the precedences and associativities

The nominal type ids are numbered since 0, for instance,

```ocaml
infixr 2 `cons` in
let m1 =
    {
        list: nom,
        maybe: nom,
        succ: int -> int,
        cons: forall a. a -> list a -> list a,
        nil : forall a. nil
    }
```
No matter the actual type id of `list`, `maybe` is, in the `.remuic`, their ids must be
`0`, `1`.

Note, for a value in the record, its name is the field name of the record.
There is an ordered arrangement for the mapping from record field names to the values,
but it's natural for the compiler, thus no need to specify it in `.remuic` files. For above
code, we can know there's a fixed order in the module `m1`, to map `succ` to that `int->int` function, etc. The order can be dictionary order of field names.
