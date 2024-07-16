#Python #Python/dictionaries #Deletion
### with keyword DEL

```python
# using keyword
del dictionary_name[key]
```

### using pop

this will remove the key, but save the removed value

```python
dictionary_name.pop(key)

# to avoid KeyError and return custom message on error
my_information.pop('nonexistant_key','Not found')

```
### using popitem()

popitem() method takes no arguments, removes and returns the last key-value pair from a dictionary.

```python
my_dictionary.update(key1= 'value1', key2 = value2, key3 = "value3")

popped_item = my_information.popitem()
# returns (key3 = "value3")
```
