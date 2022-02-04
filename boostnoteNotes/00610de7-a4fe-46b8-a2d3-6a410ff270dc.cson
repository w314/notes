createdAt: "2021-03-23T15:17:50.639Z"
updatedAt: "2021-03-23T16:26:51.971Z"
type: "MARKDOWN_NOTE"
folder: "7869a5810e7871ff4be9"
title: "JavaScript DOM"
tags: [
  "js"
  "dom"
]
content: '''
  # JavaScript DOM
  
  ## Add Element
  
  To avoid extra `reflows` create fragment, add elements to fragment before adding fragment to page.
  ```javascript
  const fragment = document.createDocumentFragment();  // ← uses a DocumentFragment instead of a <div>
  
  for (let i = 0; i < 200; i++) {
      const newElement = document.createElement('p');
      newElement.innerText = 'This is paragraph number ' + i;
  
      fragment.appendChild(newElement);
  }
  
  document.body.appendChild(fragment); 
  // reflow and repaint here -- once!
  ```
  
  Adding attributes
  ```javascript
  const element = document.createElement('p');
  element.setAttributue('id', 'elementId');
  ```
  
  ### Add Class
  ```javascript
  const div = document.createElement('div');
  div.className = 'foo';
  
  // our starting state: <div class="foo"></div>
  console.log(div.outerHTML);
  
  // use the classList API to remove and add classes
  div.classList.remove("foo");
  div.classList.add("anotherclass");
  
  // <div class="anotherclass"></div>
  console.log(div.outerHTML);
  
  // if visible is set remove it, otherwise add it
  div.classList.toggle("visible");
  
  // add/remove visible, depending on test conditional, i less than 10
  div.classList.toggle("visible", i < 10 );
  
  console.log(div.classList.contains("foo"));
  
  // add or remove multiple classes
  div.classList.add("foo", "bar", "baz");
  div.classList.remove("foo", "bar", "baz");
  
  // add or remove multiple classes using spread syntax
  const cls = ["foo", "bar"];
  div.classList.add(...cls);
  div.classList.remove(...cls);
  
  // replace class "foo" with class "bar"
  div.classList.replace("foo", "bar");
  ```
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
