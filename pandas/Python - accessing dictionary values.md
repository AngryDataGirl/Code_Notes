
#Python/dictionaries #Dictionary/Values
### view all values

```python

print(my_dictionary.values())

```

### access values

### access single value with a key

```python

#access the value associated with the given key

print(my_dictionary['key_name'])

```

### access single value with a key that does not exist

results in a KeyError

```python

# One way to avoid this from happening is to first search to see if the key is in the dictionary in the first place.

my_dictionary = {'key1': 'value1', 'key2': value2, 'key3': 'value3'}

  

#search for the 'key4' key

print('key4' in my_information)

  

# will return False since there is no Key4

```

### use get() to access value

```python

print(my_dictionary.get('value4'))

# returns none if it does not exist

  

print(my_dictionary.get(), 'This value does not exist'))

#returns message instead of None

```
