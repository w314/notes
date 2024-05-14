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

// get sublist
// end index excluded
List<Integer> slice = arrList.subList(0, 2);

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

// int[] arr to ArrayList
int[] arr9 = {1, 2, 3, 3};
List<Integer> arrList9 = new ArrayList<>(Arrays.stream(arr9).boxed().collect(Collectors.toList()));

```
