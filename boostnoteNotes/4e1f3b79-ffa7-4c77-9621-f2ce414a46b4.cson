createdAt: "2020-04-20T18:13:30.095Z"
updatedAt: "2020-04-20T20:00:40.929Z"
type: "MARKDOWN_NOTE"
folder: "0502aa55141f2315e808"
title: "Divide and Conquer"
tags: [
  "divide_and_conquer"
  "algorit"
]
content: '''
  # `Divide and Conquer`
  
  - The algorithm breaks the problem into sub-problems that can be more easily solved.
  - Also called `Recursive Algorithm`
  - Used in:
    - `binary search`
    - `merge search`
  
  ### How to find a median element of an array of unsorted numbers.
  
  Problem:
  Given an unsorted list A=[a~1~, ..., a~n~] of `n` numbers find the median of `A`.
  
  For odd `n` where `n = 2l + 1` median is the (l+1)^th^ smallest element. (Which means there are `l` elements that are at most this median element, and `l` element that are at least this median element.)
  
  ### To make the problem more general
  Given unsorted `A` and integer `k` where `1 <= k <= n` find the k^th^ smallest of `A`
  
  #### Eeasy algorithm
  - sort `A`
  - output the k^th^ element
  - total runtime `O(nlogn)`, with merge sort
  - Can we do better, like O(n)?
  
  #### Divide and Conquer QuickSort style
  - the challenge is to find a good `pivot`
  - with a bad pivot, like smallest or largest elements it would be O(n^2^)
  - with the perfect pivot (the median) O(nlogn)
  - how can we take that down to O(n)?
  - we realize that we don't have to recursively search both sides of the split array only one of them
  
  *example*
  A = [5, 2, 20, 17, 11, 13, 8, 9, 11]
  - let's chose `11` as `pivot`
  p = 11
  - let's create 3 arrays:
  A~<p~ = [5, 2, 8, 9] , A~=p~ = [11, 11], A~>p~ = [20, 17, 13]
  - Depending on the `k` the k^th^ element we are searching for is in one of those buckets, we can figure out in which one based on how big those arrays are.
    - in: A~<p~ = [5, 2, 8, 9] if k <= 4
    keep searthing for the k^th^ smallest in this array
    - in: A~=p~ = [11, 11] if 4 < k <= 6
    we can output 11
    - in: A~>p~ = [20, 17, 13] if k > 6 
    we searth for the (k-6)^th^ smallest in this array
  - we only recurse in max one array, while quicksort would sort both arrays bigger and smaller than pivot
  - 
'''
linesHighlighted: []
isStarred: false
isTrashed: false
