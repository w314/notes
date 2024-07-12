java, regex

# Regex API

## Methods using regex
- .matches()
- .split()
- .replaceFirst()
- .replaceAll()


### `.matches()`
```java
String regex = "Hello";
String input = "Hello";

System.out.println(input.matches(regex));  //true
//OR
System.out.println(Pattern.matches(regex, input)); // true
```

### `.split()`

```java
String str = "once-upon-a-time";
String regex = "-";

String words = str.split(regex);
// ["once", "upon", "a", "time"]

```

## Regex rules
- **literals**: literal characters
- **meta characters**: reserved characters with special meaning
- **quantifiers**: specify the frequency of occurance of a character or group


- `\w` = [a-zA-Z_0-9]
- `\W` = [^a-zA-Z_0-9]
- `\d` = [0-9]
- `\D` = [^0-9]
- `\s` = [\t\n\f\r] (white-space characters)
    - `\t` -tab
    - `\n` - new line
    - `\f` - form feed (old way to show page break)
    - `\r` - carriage return (brings to cursor to the starting of the current line)
- `\S` = [^\t\n\f\r]

### backreferences

```java
String pattern = "(word1) (word2) \\2 \\1";
```
In this pattern: 
- (word1) is the first capturing group
- (word2) is the second 
- `\\2` refers back to whatever was matched by the second group (word2)
- `\\1` refers back to whatever was matched by the first group (word1)
- so, this pattern is looking for a sequence of "word1 word2 word2 word1"