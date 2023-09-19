java, HashMap

- `import java.util.HashMap;`
- store key-value pairs
- similar to HashTable bu `unsynchronized`
- allows to store one `null` key
- order or elements are not guaranteed

needs:

```java
import java.util.HashMap;
```

```java
// create
// only works with wrapper types not primitives
HashMap<String, String> map = new HashMap<>();

// add element
// if you try to insert duplicate key it overwrites the previos value
map.put("TX", "Texas");
map.put("GA", "Gerogia");

// access element returns NULL if no such element
String state = map.get("TX");

// check for key
boolean hasKey = map.containsKey("TX");
// check for value
boolean hasValue = map.containsValue("Texas");


// modify element: use PUT it overrites previous value
map.put("GA", "Florida");


// remove element
map.remove("GA");
// remove all elements:
map.clear();

// iterate over
for(Map.Entry<String, String> entry: map.entrySet()) {
    System.out.println(entry); // TX=Texas
    System.out.println(entry.getKey()); // TX
    System.out.println(entry.getValue()); // Texas
}
// OR use map.keySet()


// size of array
int mapSize = map.size();

// print
System.out.println(map);

```
