createdAt: "2020-04-15T19:32:58.554Z"
updatedAt: "2020-04-15T21:17:42.898Z"
type: "MARKDOWN_NOTE"
folder: "0502aa55141f2315e808"
title: "Big O Notaion"
tags: [
  "O"
  "big_O_notation"
]
content: '''
  # Big O Notaion
  
  ## Why is binary search is O(logn) and not O(log~2~n)?
  
  
  When you change the base of logarithm the resulting expression differs only by a constant factor which, by definition of Big-O notation, implies that both functions belong to the same class with respect to their asymptotic behavior.
  
  For example
  log~10~n = log~2~n / log~2~10 = Clog~2~n
  where C = 1 / log~2~10.
  
  So log~10~n and log~2~n differs by a constant C, and hence both are true:
  log~10~n is O(log~2~n)
  log~2~n is O(log~10~n)
  In general logan is O(logbn) for positive integers a and b greater than 1.
  
  Another interesting fact with logarithmic functions is that while for constant k>1, n^k^ is NOT O(n), but logn^k^ is O(logn) since logn^k^ = klogn which differs from logn by only constant factor k.
'''
linesHighlighted: [
  5
]
isStarred: false
isTrashed: false
