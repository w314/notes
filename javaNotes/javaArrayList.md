java, ArrayList

need:

```java
import java.util.ArrayList;
```

```java


// create ArrayList
// only works with wrapper types not primitives
List<String> arrList = new ArrayList<>();

// add element
arrList.add("bob");
arrList.add("bob2");

// modify element
arrList.set(0, "bobek");

// get element
String name = arrList.get(1);

// remove element
arrList.remove(1);
// remove all elements:
arrList.clear();

// iterate over array
for(String name : arrList) {
  System.out.println(name);
}

// size of array
int arrListLength = arrList.size();


// sort array
Collections.sort(arrList);
Collections.reverse(arrList);

// search sorted arrayList<Integer>
// sort arrayList first
Collections.sort(arrList);
// returns index of element if found
int indFound = Collections.binarySearch(arrList, 9);
// returns (-(insertion point) - 1) if not found


// print array
System.out.println(arrList);

```
