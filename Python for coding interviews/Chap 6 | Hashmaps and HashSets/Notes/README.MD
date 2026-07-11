# Hashmaps and Hashsets 

## Hashmap Basics

### What is a hashmap ? 

- a hash map is a collection of key-value pairs 
- each key is unique and it maps to a specific value 
- key may be of any immutable type 

### Common Operations on a hash map 

##### Insertion : 

- insert a key-value pair into a hashmap 

  ```python
  my_dict = {}
  my_dict["a"] = 1 {"a":1}
  ```

- Time Complexity :O(1)

##### Access : 

- Access the value associated with a key

  ```python
  my_dict ={"a":1}
  print(my_dict["a"]) # 1
  ```

- Time Complexity :O(1)

##### Deletion

- delete a key-value pair from the hash map 

- There are 2 ways to delete a key-value pair from a hash map : using the `del` keyword or the `pop()` method .The only difference is that the `pop()` method returns the value associated with the key .If the key does not exist both `pop()` and `del` will raise a `KeyError` .To avoid this we can pass a default value to the `pop()` method which will be returned if the key does not exist 

  ```python 
  my_dict ={"a":1,"b":2}
  del my_dict["a"] # {"b": 2}
  my_dict.pop("b") # {}
  my_dict.pop("c") # KeyError :"c"
  my_dict.pop("c","default") # No Error , returns 'default'
  ```

- Time Complexity : O(1)

##### Lookup 

- check if a key exists in the hash map 

  ```python
  my_dict = {'a':1}
  does_a_exist = 'a' in my_dict # True 
  does_b_exist = 'b' in my_dict # False
  ```

- For lookup operations we use the `in` operator similar to how we would check if an element is in a list 

- Time Complexity : O(1)

## Default Dict 

### Straightforward way to count the frequency of elements in a list or a string 

```python
nums = [1,2,4,3,2,1]
freq = {}
for num in nums: 
  if num in freq:
    freq[num]+= 1
  else:
		freq[num] = 1
    
print(freq) # {1:2, 2:2,4:1,3:1}
```

### Better Solution

- Python provides a more elegant way to do this using the *collections* module 

- The *collections* module provides a class called *defaultdict* that is a subclass of the built in *dict* class 

- It allows us to set a default value for a key that doesn't exist in the dictionary .This can be very useful when counting the frequency of elements in a list

  ```python
  from collections import defaultdict
  
  nums = [1,2,4,3,2,1]
  freq = defaultdict(int)
  
  for num in nums:
    freq[num]+=1
  print(freq) # {1:2,2:2,4:1,3:1}
  ```

- We created a `defaultdict` and passed in `int` as the default value .This means that if a key doesn't exist in the dictionary , it will be created with a default value of the integer `0` .This allows us to increment the value without checking if the key exists 

### Similar Pattern

```python
nums = [1,2,4,3,2,1]
d = defaultdict(list)
for num in nums:
  d[num].append(num)
  
print(d) # {1:[1,1],2:[2,2],4:[4],3:[3]}
```

Explanation ➡️

- The above code creates a dictionary where each key is a number in the list and the value is a list of all the occurrences of that number .Even if the number doesn't exist in the dictionary , it will first create an empty list as the default value and then append the given value `num` to the list

## Counter 

- to count the occurrences of elements in a list an even better solution exists then the `defaultdict` .We use the `collections.Counter` class : 

  ```python
  from collections import Counter 
  nums = [1,2,4,3,2,1]
  
  counter = Counter(nums)
  print(counter) # Counter ({1:2, 2:2,4:1,3:1})
  counter[100] +=1 # No error , even though 100 is not a key 
  print(counter) # Counter ({1:2.2:2,4:1,3:1,100:1})
  ```

- The `counter` class is a subclass of the `dict` class and it provides a more concise way to count the occurrences of elements in a list. It returns a dictionary where the keys are the elements in the list and the values are the number of times each element appears .It behaves similarly to a `defaultdict` with an integer default value meaning if a key doesn't exist , it will return `0` 

  ### Counting the occurrence of multiple lists or strings 

  - we use the `update()` method 

    ```python
    nums1 = [1,2,4,3,2,1]
    nums2 = [1,2,3,4,5]
    counter = Counter(nums1)
    counter.update(nums2)
    print(counter) # Counter ({1:3, 2:3 , 4:2 , 3:2 , 5:1 })
    ```

## Dict Comprehension 

- We can use dictionaries comprehensions to initialize dictionaries in a more concise way 

```python
nums = [1,2,3,4,5]
squared = {num: num * num for num in nums }
print(squared) # {1:1 ,2:4 , 3:9 ,4:16 ,5:25}
```

- we created a dictionary where the keys are the numbers from the list `nums` and the values are the squares of each number

## Dict Items 

### Getting all the keys from a dictionary 

- The `keys()` method returns a view object that displays a list of all the keys in the dictionary .We can convert this view object to a list using the `list()` method 

```python
my_dict = {'a':1,'b':2 ,'c':3}
keys = my_dict.keys()
print(keys) # dict_keys (['a','b','c'])
keys_list = list(keys)
print(keys_list) # ['a','b','c']
```

### Getting all the values from a dictionary using the `values()` approach

- Similar approach 

  ```python
  my_dict ={'a':1,'b':2,'c':3}
  values = my_dict.values()
  print(values) # dict_values ([1,2,3])
  values_list = list(values)
  print(values_list) # [1,2,3]
  ```

### Getting all the key-value pairs from a dictionary using the `items()` method 

```python
my_dict  = {'a':1,'b':2,'c':3}

for key,value in my_dict.items():
  print(key,value)
```

## Hash Sets 

### Main Points 

- Hash sets cannot contain duplicates 
- In Python , hash sets are implemented using the `set` class 

The common operations on a hash set 

- insertion : insert a key into the hash set 

  - Time Complexity : O(1)

  ```python
  my_set = set()
  my_set.add('a') # {'a'}
  ```

- deletion : delete a key from a hash set 

  -   Time Complexity : O(1)

    ```python
    my_set = {'a'}
    my_set.remove('a') # {}
    my_set.remove('a') # KeyError
    
    my_set.add('b') # {'b'}
    my_set.discard('b') # {}
    my_set.discard('b') # {} (No error)
    ```

    - We can use the `remove()` method to delete an element from a hash set . If the element does not exist the method will raise a `KeyError` . Alternatively we can use the `discard()` method which will not raise an error if the element does not exist 

  -  Lookup : check if a key exists in the hash set 

    - For lookup operations we can use the `in` operator 

    - Time Complexity : O(1) 

      ```python
      my_set ={'a'}
      'a' in my_set # True
      'b' in my_set # False
      ```

  ## Set Comprehension

  ```py
   nums = [1, 3, 5]
  
  squared = {num * num for num in nums}
  
  print(squared)  # {1, 9, 25}
  ```

  - In the above code, we created a set where the elements are the square of each number in the list `nums`. Notice that the syntax is similar to list comprehension, but we use curly braces instead of square brackets. Inside the curly braces, we have the expression we want to add to the set.

  ​    

  ## Tuple Keys 

  -  It's common to store pairs of values in a dictionary or set. For example, we might store the `row, column` pair of a cell in a grid. While we cannot store a list as a key in a dictionary, we can use a tuple instead.

    ```py
    dict_of_pairs = {}
    
    dict_of_pairs[(0, 0)] = 1
    dict_of_pairs[(0, 1)] = 2
    
    print(dict_of_pairs)  # {(0, 0): 1, (0, 1): 2}
    
    set_of_pairs = set()
    
    set_of_pairs.add((0, 0))
    set_of_pairs.add((0, 1))
    
    print(set_of_pairs)  # {(0, 0), (0, 1)}
    ```

  - In the above code, we created a dictionary and a set where the keys and elements are tuples. We can use tuples to store pairs of values in a single object. This is useful when we want to store multiple values together, but we don't want to create a new class or structure.