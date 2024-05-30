java, array

## Java Arrays

> What is an array? Why is it useful?
- data structure
- a `contiguous block of memory` storing a group of `sequentially stored` elements of the same type
- provides fast data access.
- fixed size and cannot be resized after declaration
- indexed - items in an array are referenced via their index in square bracket notation, which begins with 0 for the first element
- have a length property specifying the length of the array
- can be iterated over

```java
// CREATE

// create empty array with 5 elements
int[] myArray = new int[5];

// OR one with values
int[] otherArray = {1, 2, 3};


// ADD ELEMENT
//FIXED SIZE CANNOT ADD


// modify element
int[] arr1 = {4, 5, 6}
Arrays.fill(arr, 2);
arr[1] = 5;


// GET ELEMENT
int n = arr[2];


// REMOVE ELEMENT
// FIXED SIZE CANNOT REMOVE


// SUBARRAY
int[] nums = {45, 67, 12};
// end index excluded
int[] slice = Arrays.copyOfRange(arr, startIndex, endIndex);

// iterate over array
for(int n : arr) {
  System.out.println(n);
}

// length of the array
// PROPERTY not method
myArray.length;

// print out array
System.out.println(Arrays.toString(myArray));

```

> How can you iterate over an array?

> How would you access the last value in an array if you do not know the size of the array?

#### Arrays Static Methods

- `Arrays.sort()` - modifies original array
- `Aarrays.binarySearch()` - array must be sorted
- `Arrays.toString()` - for printing out array
- `Arrays.equals(array1, array2)` - compares the contents of the arrays


```java
// sort array
Arrays.sort(arr);

// SEARCH ARRAY

int[] arr2 = {6, 9, 7};

// sort array first
Arrays.sort(arr2);

// search, returns index of element if found
int indFound = Arrays.binarySearch(arr2, 9); 
// returns 2

// returns (-(insertion point) - 1) if not found
int indNotFound = Arrays.binarySearch(arr2, 8); // returns -3


// compare array contents
boolean sameContent = Arrays.equals(arr1, arr2);

// slice array
int[] nums = {2, 5, 7, 8};
int[] nums2 = Arrays.copyOfRange(nums, 1, 3);
int[] nums3 = Arrays.stream(nums, 1, 3).toArray(int[]::new);

// print array
System.out.println(Arrays.toString(arr));



// ARRAY -> ARRAYLIST 

// for string arrays - does not work with int[] to List<Integer>
String[] arr3 = {"bob", "bobek"};
List<String> arrList = new ArrayList<>(Arrays.asList(arr3));
// OR
List<string> arrList1 = new ArrayList<>();
Collections.addAll(arrList1,arr3);

// for arrays of primitives
int[] arr4 = {1, 2, 5};
List<Integer> arrList4 = new ArrayList<>(Arrays.stream(arr4).boxed().toList());
// - boxed wraps the object to its wrapper object



// ARRAY -> SET

// string array
String[] strArr = {"nn", "mm", "mm", "oo"};
Set<String> strSet = new HashSet(Arrays.asList(strArr));

// with primitives
int[] arr5 = {3, 4, 4, 5};
Set<Integer> arrSet = new HashSet<>(Arrays.stream(arr5).boxed().toList);

```


> What is the difference between an array and an ArrayList?
