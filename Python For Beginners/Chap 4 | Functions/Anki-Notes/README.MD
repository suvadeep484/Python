# Functions

Anki : 04-functions

```python
def add(x:int,y:int)->int:
  return x + y

print(add(2,5)) # 7
```

**Q**: What is local scope ? 

**Solution**:

varibles defined inside the function are only accessible within the function(x,y)

**Q**: What are parameters ? 

**Solution**:

inputs to the function definition are called parameters 

**Q**: What are called arguments ? 

**Solution**:

inputs passed to the function call are called arguments 

**Q**: What are Type Hints ? 

**Solution**: 

indicates what type of data the function expects to receive and return , this is optional 

**Q**: What is Global Scope ? 

**Solution**:

variables declared outside of any function have a global scope and they can be accessed from the program including inside functions