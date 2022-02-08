createdAt: "2021-01-29T16:47:57.055Z"
updatedAt: "2021-01-29T17:08:03.977Z"
type: "SNIPPET_NOTE"
folder: "096077ec96120ea00fda"
title: "Classes"
tags: [
  "class"
]
description: "Classes"
snippets: [
  {
    linesHighlighted: []
    name: "classPython.py"
    content: '''
      class Person:
        def __init__(self, name, age):
          self.person_name = name
          self.person_age = age
          
        def birthday(self):
          self.person_age += 1
          
        def getName(self):
          return self.person_name
        
      
      bob = Person('Bob', 32)
      print(bob.getName())
      
    '''
    mode: "Python"
  }
  {
    linesHighlighted: []
    name: ""
    content: ""
  }
]
isStarred: false
isTrashed: false
