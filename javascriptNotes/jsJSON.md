# JSON

## Commenting in JSON file

Write your comments like regular json members. 
[Source](https://stackoverflow.com/questions/14221579/how-do-i-add-comments-to-package-json-for-npm-install)
```json
{
    "type": "module",
    "comments": {
        "type": "allows for using import syntax"
    }
}
```

OR

```json
{ 
  "//": "comment!", 
  "dependencies": {...}
} 
```
Can only be used at the **root** of the `package.json` object.

The following is NOT valid:
```json
{ 
  "dependencies": { 
     "//": "comment?" 
  }
}
```