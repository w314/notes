createdAt: "2020-04-15T19:14:47.181Z"
updatedAt: "2020-04-22T20:02:50.528Z"
type: "MARKDOWN_NOTE"
folder: "0502aa55141f2315e808"
title: "Trees"
tags: [
  "data_structure"
  "tree"
  "binary_tree"
  "binary_search_tree"
  "bst"
  "heap"
]
content: '''
  # Trees
  - is extension to `linked lists`
  - individual elements contain value and often called `nodes`
  - the first element is called a `root`
  - the nodes in the tree can have several next elements
  - rules of a tree:
      - a tree must be completely connected (starting from the root there must be some way to reach every node)
    - there must not be any cycles in the tree
  ### tree terminology:
    - `level`: how many connections it takes to reach the `root` + 1 (root is level 1)
    - `parent - child` relationship: a node connected at a higher level is a `child` of the `parent` node it's connected to at the lower level
      - each `child` is allowed only one `parent`
      - if a `parent` has multiple `children` they are called `siblings`
      - you can talk about the same as `ancestor` and `desendants`
    - `leaves` are the nodes at the end that don't have any children or `external nodes`
    - `parent` nodes are called `internal nodes`
    - a connection between two nodes is an `edge` a group of connections taken together a `path`
    - `height of a node` is a number of edges between it and the furthest `leaf` of the tree
      - `leaf` has a `height` of 0
      - `parent` of a `leaf` has `height` of 1
      - `height of a tree` = height of the root node
    - `depth of a node` is a number of edges to the `root`
      - `height` and `depth` go inversely
  ## `tree traversal`
  - xxxxxxxxx`D`xxxxxxx
  - xxxx`B`xxxxxxx`E`xx
  - xx`A`x`C`xxxxxxx`F`
    - `DFS` (Depth First Search) : if there children nodes to explore explore them first
    - `BFS` (Breadth First Search) : priority is visiting every node on the level we are currently on before visiting any child nodes
  - tree traversal is used for search, insertion, deletion
  ### `BFS` (Breadth First Search)
  ##### `Level Order Traversal`
    - `Level Order` traversing is a `BFS` with a more exact algorithm
    - start at the `root`
    - visit levels one by one starting from the left most side of the level and move right
  
  ### `DFS` (Depth First Search)
  ##### `Pre Order Traversal`
  - `pre` means: check off a node as soons as you see it before you taverse any further into the tree (vs checking off a node's children first before checking off the node itself)
  - we start at the `root` and check it off immideately
  - move on the left child and check it off
  - continue traverse down the left most nodes until reaching a leaf (checking off each nodes as we go through it)
  - check off the `leaf` traverse back the `parent` and check off the next child of the parent
  - D B A C E F
  #### `In Order Traversal`
  - we are moving through the nodes in the same order as in pre order traversal
  - but we are only checking off a node if we have seen it's left child and came back to it
  - start at the `root` but don't check it off yet as we have not seen the left child yet
  - move til you find the first `leaf`, check off the `leaf`
  - move up to the parent, as we have seen its left child we can check off the parent now
  - move to the right child
  - A B C D E F (as F is a right child it's visited after the parent)
  - this moves trhough the tree in order from left to right
  ##### `Post Order Traversal`
    - you cannot check off a node until you have visited all of its desendants
    - start at the root, dont check it off but find the leftmost leaf
    - check off the leaf move to the parent, but don't check it off but go the next child first
    - once all the children are checked off check off the parent
    - A C B F E D
  ## `Binary Tree` (with no order)
    - trees where parents have at most two children
    - ab`complete binary tree` is one where all levels except the last one is completely full. If the last one is not completely full values are added from left to right
    - `search` in a binary tree:
      - can use any of the traverse algorithm
      - as there is no order to the nodes may have to go through all nodes to find the one we are looking for
      - O(n)
    - `delete` in binary tree:
      - search for the element
      - remove the element
      - if it is not a `leaf` replace it with one of it's children or children's
        - you cannot create a situation where nodes have more than two children
        - may have to traverse to find a leaf to replace the deleted element with, as there is no order to the elements it is no problem
        - O(n)
    - `insert` in to the tree
      -  tuck the new node to an other node
      -  just make sure to obey the max two children rule
        -  start at the root and move down the tree until you find an open spot
      -  O(logn)
  ## `Binary Search Tree (BST)`
    - type of binary tree
    - sorted every value of the left of a particular node is smaller then it and on the rigth is larger than it
    xxxxxxxxx`5`xxxxxxx
    xxxx`3`xxxxxxx`8`xx
    xx`1`xxxxxxx`7`x`9`x
    - `search` in binary tree
      - O(logn) 
      - when serching for '7', we start at root see that 7 > 5
      - go to the right as 8 < 7 to the left ....
      - we only have to traverse the `height` of the tree
    -`insert` into `BST`
      - O(logn)
    - `deleting` from `BST`
      - O(logn)
    - `unbalanced binary search tree`
      `5`
      xx`10`
      xxxxx`15`
      - while average search is O(logn)
      - these unbalanced trees are worst case scenarios whith search O(n)
  ## `Heap`
    - special type of tree
    - not necessary binary, parents can have any number of children
    - in a `heap` elements are arranged in increasing or decreasing order
    - the `root` element is either the maximum(`max heap`) or minimum (`min heap`)value in the tree
    - in a `max heap` a parent always have to have greater value than its children:
    xxxxxx`7`xxxxxxx
    xxx`5`xxx`3`xxxx
    x`2`x`1`xxxxxxxx
    - in a `min heap` parent has lower value, than children
    - `heapify` when we reorder the tree based on the `heap property`
      - will keep comparing our element to it's parent and swap them until we find the right spot for them
    
  ##### complete binary max heap
    - search for a max value `peek` happens in constant time O(1)
    - search in general: we don't have to search a subtree is our value is bigger than it's parent
      - average case O(n/2) (wich is still lienar O(n))
      - worst case O(n)
    - insert:
      - stick the new element in the first open spot
      - than `heapify`
    - `extract` (remove the root)
      - remove root
      - replace it with the rightmost leaf
      - heapify (compare to child element and swap if needed until we find the right spot for it)
      - worst case: O(logn), the height of the tree
  ### implementation of a heap
  - though `heaps` are represented as `trees`, they are often stored as `arrays`
  
  
      
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
