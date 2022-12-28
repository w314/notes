react, typescript, error

# Read TypeScript Errors

Error: 

Type '({ todos }: TodoListProps) => Element[]' is not assignable to type 'FC<TodoListProps>'. Type 'Element[]' is missing the following properties from type 'ReactElement<any, any>': type, props, key

[solution](https://stackoverflow.com/questions/58898227/type-items-propswithchildrentodoprops-element-is-not-assignable):

Enclose returned code in `<React.Fragment>` or simply `<></>`
