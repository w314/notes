java, HashMap

- `import java.util.HashSet`
- no duplicates

```java
// create
// only works with wrapper types not primitives
HashSet<String> set = new HashSet<>();

// add element
// no error if you try to add already existing element
set.add("TX");

// check for element
boolean hasElement = set.contains("TX");


// remove element
set.remove("GA");
// remove all elements
set.clear();


// get size
int setSize = set.size();

// iterate over
for(String element : set) {
    System.out.println(element);
}

// print
System.out.println(set);

// array to set
String[] arr1 = {"TX", "GA"};
HashSet<String> set1 = new HashSet<>(Arrays.asList(arr));
// with primitives
int[] arr2 = {3, 5, 6, 6};
HashSet<Integer> set2 = new HashSet<>(Arrays.stream(arr2).boxed().collect(Collectors.toSet()));



```
