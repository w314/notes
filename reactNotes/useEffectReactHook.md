react, useEffect, hooks

# `useEffect()` react hook

Resources:
- [web-dev-simplified intro](https://www.youtube.com/watch?v=0ZJgIjIuY7U&t=529s)
- [jack harrington: mastering useEffect](https://www.youtube.com/watch?v=dH6i3GurZW8&t=126s)
  

My projects:
- [reactUseEffectExample](https://github.com/w314/reactUseEffectExample)

>Use `useEffect()` when you want to react to anything that changes.

```typescript
// set up event listener to track window width change
// use empty array as parameter to set it up only once when the application mounts
useEffect(() => {
    console.log('setting up event listener')
    window.addEventListener('resize', handleResize)

    // return is our clean up
    // it is run when the component unmounts and 
    // every time the component rerenders before the main code is run
    // we remove the eventlistener on return to avoid registering a new event listener
    // every time the app rerenders
    return () => {
      console.log('removing event listener')
      window.removeEventListener('resize', handleResize)
    }
  }, [])
```
