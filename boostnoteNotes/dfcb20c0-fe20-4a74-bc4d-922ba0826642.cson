createdAt: "2020-04-15T21:47:23.251Z"
updatedAt: "2020-04-17T17:06:45.720Z"
type: "MARKDOWN_NOTE"
folder: "0502aa55141f2315e808"
title: "Sorting Algorithms"
tags: [
  "sorting"
  "algorithm"
]
content: '''
  # Sorting Algorithms
  
  - `naive approach`: compare each element to every other element
  - any sorting algorithm can be `in place` (low space complexity) or not
   ## `Bubble Sort` (or `Sinking Sort`)
   - `naive` approach
   - `in-place`, so `space complexity` is constant: `O(1)`
   - uses comparisons
     - starting with the first element is compares them, if the first is bigger switches them if needed
     - keeps comparing each array element to the next one
     - the largest value should "bubble up" at the end
     - repeats the process until only the first to elements needs to be compared
   - `time complexity`:
     - average & worst case: `O(n^2^)`
     - best case: `O(n)`
  
  ## `Merge Sort`
  - split the array, sort the parts and build it back again (this strategy is called `Divide & Conquer`)
  - method:
    - split the array to arrays one element each
    8|3|1|7|0|10|2 -> 8 3 1 7 0 10 2
    - create pairs and sort them into two elements array
    8 1|3  0|7  2|10
    - keep moving:
    1|3|8  0|2|7|10
    ->
    0|1|2|3|7|8|10
  - `time complexity`: `O(nlogn)` as we are doing n comparisons in logn steps
  - `space efficiency`: O(n) (= Auxiliary Space), as we need new arrays all the time, even as we delete the old arrays we have created in the meantime
  
  ## `Quick Sort`
  - in many cases one the most efficient sorting algorithm
  - `in-place`
  - method
    - select a `pivot` a value in the array at random, conventionally we pick the last element
    - move all values larger than it below it
    - move all values smaller than it above it
    - continue recursively picking a pivot in the upper and lower section of the array, sorting them similarly until the whole array is sorted
    - step by step:
      - 8|3|1|7|0|10|2 pivot: `2`
      - we compare it to the first element of the array, as `8` > `2` we have to move it after `2`. As it's `in place` sort to do that we:
        -  move `8` to the last block
        - `2` to the second to last block
        - `10` to the first block
    10|3|1|7|0|2|8
      - next we compare with the first element of the array agein, as `10` > `2`:
      0|3|1|7|2|10|8
      - check first element again as `0` < `2`, it's at its right place and we move to the second element of the array to compare
      - `3` > `2` ->
      0|7|1|2|3|10|8
      - keep comparing the second element of array, `7` > `2` ->
      0|1|2|7|3|10|8
      - finally check the second element once more as `1` < `2` and there no elements uncompared in the array before our `pivot` this round is done
      - as now everythin before `2 `is smaller than `2` and everythin after `2` is larger than `2`, we know that `2` is exactly at the right place
      - we repeat the whole process in both parts of the array the before `2` and the after `2` part
        - select the last element of the array part as `pivot`
        - compare and move elements as needed
  - time efficiency
    - worst case: `O(n^2^)`, if the array as already in the right order we have to compare all values to all other values
    - average case: `O(nlogn)`, when we can move the pivots to the middle and half the array at each step
    - therefore it's not efficient to use quick sort for nearly sorted arrays
  - making quick sort more efficient
    - after splitting the array make your program process both halves at the same time, it will require more processing power but less time
    - instead of selecting the last element as a pivot look at the last few elements and select their median
  - space complexity: `O(1)` as it's an `in-place` sorting method
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
