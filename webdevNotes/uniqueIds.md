unique, id, uudv4

# How to create unique ids

Resources
- [how to generate unique keys for react lists](https://blog.devgenius.io/the-quicky-lazy-but-effective-way-to-create-unique-keys-for-react-elements-e45d574028a3)
- [uuids explained](https://www.sohamkamani.com/uuid-versions-explained/)
- [uuid](https://www.npmjs.com/package/uuid)


Install:
```bash
yarn add uuid @types/uuid
```
Use:
```typescript
import { v4 as uuidv4 } from 'uuid'

const id = uuidv4()
```