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


// ADD ELEMENT
// if you try to insert duplicate key it overwrites the previos value
map.put("TX", "Texas");
map.put("GA", "Gerogia");


// MODIFY ELEMENT
//use PUT it overrites previous value
map.put("GA", "Florida");


// REMOVE ELEMENT
map.remove("GA");
// remove all elements
map.clear();


// ACCESS ELEMENT
// returns NULL if no such element
String state = map.get("TX"); // Texas


// CHECK FOR EXISTENCE OF KEY
boolean hasKey = map.containsKey("TX");


// CHECK FOR EXISTENCE OF VALUE
boolean hasValue = map.containsValue("Texas");


// ITERATE OVER ELEMENTS
for(Map.Entry<String, String> entry: map.entrySet()) {
    System.out.println(entry); // TX=Texas
    System.out.println(entry.getKey()); // TX
    System.out.println(entry.getValue()); // Texas
}


//  ITERATE OVER KEYS
for(String key : map.keySet()) {
    System.out.println("Key = " + key);
    System.out.println("Value = " + map.get(key));

}


// ITERATE OVER VALUES
for(String value : map.values()) {
    System.out.println(value);
}



// SIZE
int mapSize = map.size();


// PRINT
System.out.println(map);

```
