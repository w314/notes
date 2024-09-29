js, javascript, json, math, date, string, regex

# JavaScript Global Objects

## Date

```js
let today = new Date();
console.log(today);

// 2002 may 14
// month is 0 based so use 4
let dateOfBirth = new Date(2002, 4, 14);
console.log(dateOfBirth);
```


### Getter Methods
- getDate() - day of the month
- getDay() - numeric day of the week 0-6
- getFullYear() - four digit year
- getHours() - numeric hour 0-23
- getMonth() - numeric month 0-11
- getTime - number of milliseconds since 1/1/1970 12am

Same functions have setter counterparts.


## String
See `jsString.md`

## Math
> JavaScript object used to make mathematical calculations on the web.

### Properties
- `Math.PI`
- `Math.SQRT2`

### Methods
```js
Math.max(6, 7); // 7
Math.min(6, 7); // 6
Math.ceil(7.4); // 8
Math.floor(7.8); // 7
// returns any random number between 0 and 1
// inclusive 0, exclusive 1
Math.random();
Math.round(4.5); // 5
Math.sqrt(9); //3
```

## RegExp

To create RegExp patter:
```js
let pattern1 = new RegExp(pattern, modifiers);

// OR

let pattern2 = /pattern/modifiers;
```
- modifiers are optional

### Pattern rules

- `.` any single character
- `[abc]` string with any of characters present in the bracket
- `(a|b)` string with either a or b
- `[^abc]` string without a and b and c
- `?=n` match any string that is followed by the string n

#### Quantifiers
- `+` one or more
- `*` zero or more
- `?` zero or one
- `{3}` exactly 3 times
- `{3,}` at least 3 times
- `{0,3}` max 3 times 


Examples
```js
// to make sure that string has @ and .com 
let emailPattern = new RegExp("(?=.@*)(?=.+.com)");
 
//to make sure that given number has digits between 0-9 and max length of 10 digits 
let phoneNumberPattern = new RegExp("(?= [0-9]{10})"); 
//to make sure password has characters a to z, number 0-9 and special symbol @,#,$,%,!,^,&,*,+ or underscore
let passworPattern = new RegExp("(?=.*[0-9])(a-zA-Z)(?=.*[@#$%!^&*+_])");
```

### Modifiers




## JSON
> Lightweight data-interchange format.
- JavaScript Object Notation
- used for stroring and sharing data between client and servers over the network
- uses `""` for keys and strings
- text only format, travels over the network as string


### JSON Methods:

- `JSON.parse()` - JSON -> object
- `JSON.stringify()` - object -> JSON


```js
// JSON -> object
let myJSON = {"name": "bob", "pet": "dog"};
// parses a string as JSON and helps program to create an object from it
let kid = JSON.parse(myJSON);
console.log(kid) // {name: 'bob', pet: 'dog'}

// object -> JSON
let person = {name: 'rob', role: 'admin'};
// returns the object's JSON string
let personJSON = JSON.stringify(person);
console.log(personJSON); // {"name": "rob", "role": "admin"}
```

