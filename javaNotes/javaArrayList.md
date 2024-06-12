java, ArrayList
- only works with wrapper objects not primitives


needs import:

```java
import java.util.ArrayList;
```

```java
// CREATE

// empty
List<String> arrList = new ArrayList<>();
// with values
List<Integer> arrList1 = new ArrayList<>(Arrays.asList(1, 2, 3));


// ADD ELEMENT
arrList.add("bob");


// MODIFY ELEMENT
arrList.set(0, "bobek");


// GET ELEMENT
String name = arrList.get(1);


// REMOVE ELEMENT
// at index
arrList.remove(1);
// remove all elements:
arrList.clear();


// SUBARRAYLIST
// end index excluded
List<Integer> slice = arrList.subList(0, 2);


// ITERATE OVER
for(String name : arrList) {
  System.out.println(name);
}

// SIZE
int arrListLength = arrList.size();


// SORT
Collections.sort(arrList);
// reverse sort
Collections.reverse(arrList);


// search sorted arrayList<Integer>
// sort arrayList first
Collections.sort(arrList);
// returns index of element if found
int indFound = Collections.binarySearch(arrList, 9);
// returns (-(insertion point) - 1) if not found


// print array
System.out.println(arrList);


// CONVERT

// ArrayList to int[]
  List<Integer> list10 = new ArrayList<>(Arrays.asList(2, 3, 6));
  int[] arr10 = list10.stream().mapToInt(i -> i).toArray();
```
