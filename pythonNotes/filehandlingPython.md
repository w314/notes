# Working with files

## List directory content

```py
import os

# returns array of content
# with relative path
os.listdir('.')

# check for file or directory
os.path.isfile('./testfile.py')
```

## Reading from file

```python
with open('input01.txt', 'r') as f:
    length = f.readline()
    print('input length: ', length)
    num_string = f.readline()
```
