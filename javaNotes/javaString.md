java, string

- immutable
- methods return new string

```java
// create
String str = "Me bob";

// length
int strLength = str.length();

// find
// find character at index
char c = str.charAt(1);
// find index of character
int firstIndex = str.indexOf("b");
// find next occurance
int secondIndex = str.indexOf("b", firstIndex + 1);
// or find string
int strIndex = str.indexOf("bob");

// get substring
String subStr = str.substring(1);
// end index excluded
String subStr1 = str.substring(1, 4);

// check for equal content
String str2 = "Me bob";
boolean sameStr = str.equals(str2);
// OR
boolean same = str.equalsIgnoreCase(str2);

// manipulate strings
str.toLowerCase();
str.toUpperCase();
str.trim();
str.replace(char old, char new);

// concatenate strings
String newStr = str.concat("!");

// split string
// string to words array
String[] words = str.split(" ");
// string to char array
char[] letters = str.toCharArray();


// conversions
// int to String
int x = 345;
String num = String.valueOf(x);
// string to int
String n = "12";
int y = Integer.parseInt(n);



```
