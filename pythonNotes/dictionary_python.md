# Dictionary

- safely access dictionary item:
```python
est_dict = {'Gfg' : {'is' : 'best'}}
    
# printing original dictionary
print("The original dictionary is : " + str(test_dict))
    
# using nested get()
# Safe access nested dictionary key
res = test_dict.get('Gfg', {}).get('is')
    
# printing result
print("The nested safely accessed value is :  " + str(res))
```