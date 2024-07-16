
#Python/dictionaries 
### add value to dictionary

- if key already exists in the dictionary and the key will end up being updated with the new value.

- remember that keys need to be unique.

```python

# method 1

dictionary_name[key] = value

  

# method 2: built in update

my_dictionary.update(key1= 'value1', key2 = value2, key3 = "value3")

```

### add value to dictionray in a for loop

  

```python

for x in item_to_be_looped:

  if x in dictionary:

    dictionary[x] = value

```

### increment count of value in dictionary

  

```sql

for x in item_to_be_looped:

  if x in dictionary:

    dictionary[x] += value

```

