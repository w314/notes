java, HashMap
- stores key-value pairs
- allows to store one `null` key
- order or elements are not guaranteed

```java
// import is needed
import java.util.HashMap;


// CREATE MAP

// only works with wrapper types not primitives
HashMap<String, String> map = new HashMap<>();


// MANIPULATE ELEMENTS

// add element
// if you try to insert duplicate key it overwrites the previos value
map.put("TX", "Texas");
map.put("GA", "Gerogia");

// modify element: use PUT it overrites previous value
map.put("GA", "Florida");

// remove element
map.remove("GA");
// remove all elements:
map.clear();


// ACCESS ELEMENT

```java
// access element returns NULL if no such element
String state = map.get("TX"); // Texas


// CHECK FOR EXISTENCE OF ELEMENT

// check for key
boolean hasKey = map.containsKey("TX");

// check for value
boolean hasValue = map.containsValue("Texas");


// ITERATE OVER ELEMENTS


// iterate over elements
for(Map.Entry<String, String> entry: map.entrySet()) {
    System.out.println(entry); // TX=Texas
    System.out.println(entry.getKey()); // TX
    System.out.println(entry.getValue()); // Texas
}

// iterate over keys


// OR use map.keySet()

// iterate over values


// OTHER (SIZE & PRINT)

// size of array
int mapSize = map.size();

// print
System.out.println(map);

```
