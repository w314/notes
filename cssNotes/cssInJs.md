css, js, cssInJs

# CSS in JS

[About CSS in JS](https://css-tricks.com/a-thorough-analysis-of-css-in-js/)

`Atomic CSS` is giving classname to any possible CSS property used and adding those classnames to HTML element if they need them

## [Emotion](https://emotion.sh/docs/introduction)

- for using styled components install
```bash
npm i @emotion/styled @emotion/react
```

- import to `.tsx` file
```typescript
import styled from '@emotion/styled'
```

### [How to use](https://emotion.sh/docs/styled)

- can call it with a `template literal`
```javascript
import styled from '@emotion/styled'

const Button = styled.button`
  color: turquoise;
`

render(<Button>This my button component.</Button>)
```

