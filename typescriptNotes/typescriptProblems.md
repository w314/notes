typescript, error, problem,  key, string

# Typescript Problems

## When iterating over keys and values of an object 
- using `Object.keys()` gives you a `cannot use a string as a key` when trying to display `obj.[key]`

### Solution
- use [`Object.entries(yourObject)`]((https://stackoverflow.com/questions/65375043/iterate-over-objects-keys-and-values-in-typescript)) which return keys as strings and map that
```tsx
{Object.entries(pokemon.base).map(([key, value]) => 
  (<tr key={key}>
    <td>{key}</td>
    <td>{value}</td>
  </tr>)
)}
```
- you can also set type to `Record<string, number>` to specify that keys are strings.