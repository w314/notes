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


// REVERSE ORDER OF ELEMENTS
// NOT reverse sort
Collections.reverse(arrList);


// SEARCH sorted arrayList<Integer>
// sort arrayList first
Collections.sort(arrList);
// returns index of element if found
int indFound = Collections.binarySearch(arrList, 9);
// returns (-(insertion point) - 1) if not found


// print array
System.out.println(arrList);


// CONVERT
// int[] to ArrayList<Integer>
  List<Integer> list10 = new ArrayList<>(Arrays.asList(2, 3, 6));

// ArrayList<Integer> to int[]
  int[] arr10 = list10.stream().mapToInt(i -> i).toArray();
```


## ArrayList Methods

- `void add(int index, Object element)` - inserts element at position
- `boolean add(Object element)`
  - can add `null` values not just the element type
- `boolean addAll(Collection c)`
- `boolean addAll(int index, Collection c)`
- `Iterator iterator()`
<br> returns an iterator over the elements
- `void clear()`
<br> removes every element
- `boolean contains(Object element)`
- `Object get(int index)`
<br> returns element at index
- `int indexOf(Object element)`
<br> returns the first occurence of the element
- `boolen isEmpty()`
- `int lastIndexOf(Object element)`
- `Object remove(int index)`
<br> removes element at index
- `Object set(int index, Object element)`
<br> replaces current element of ArrayList at index with new element
- `int size()`
<br> returns number of elements
- `Object[] toArray()` - returns and array containing the elements
- `void sort(Comparator c)`