createdAt: "2020-07-07T17:17:20.069Z"
updatedAt: "2020-11-03T00:21:43.353Z"
type: "MARKDOWN_NOTE"
folder: "7b7225fb954665754643"
title: "WEB Performance"
tags: []
content: '''
  # WEB Performance
  
  ## `performance.now()` - Measure Performance
  - [performance.now() - Web APIs \\| MDN](https://developer.mozilla.org/en-US/docs/Web/API/Performance/now)
  ```javascript
  const t0 = performance.now();
  doSomething();
  const t1 = performance.now();
  console.log(`Call to doSomething took ${t1 - t0} milliseconds.`);
  ```
  
  
  ## `.createDocumentFragment` - Add Content Faster
  - after adding each  element to body, the browser will run through:
    - `reflow`
    The process of the browswer laying out the page. Happens at the beginning after the DOM and CSS are loaded, and every time something could change the layout. It's a slow process.
    - `repaint`
    Happens after each reflow as the browser draws a new layout. Much faster than reflow.
    
  - it can be avoided by using `.addDocumentFragment`
  ```javascript
  const fragment = document.createDocumentFragment();  // ← uses a DocumentFragment instead of a <div>
  
  for (let i = 0; i < 200; i++) {
      const newElement = document.createElement('p');
      newElement.innerText = 'This is paragraph number ' + i;
  
      fragment.appendChild(newElement);
  }
  
  document.body.appendChild(fragment); // reflow and repaint here -- once!
  ```
  
  ## Reduce `reflow`
  - Even adding a CSS class can cause reflow & repaint.
  ```html
  <div id="comments">
    <div class="comment"> <!-- some content --> </div>
    <div class="comment"> <!-- some content --> </div>
    <div class="comment"> <!-- some content --> </div>
  </div>
  ```
  - deleting two comments is two reflow and repaint
  - hide `#comments`, delete comments and show it again is much faster, just 1 reflow and 2 repaint (hiding doesn't change layout, so no need to reflow at that point)
  
  
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
