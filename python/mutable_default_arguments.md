# Mutable default arguments

__NOTE__: Information taken from [python guide](http://docs.python-guide.org/en/latest/writing/gotchas/)

One of the most confusing moments for new developers is when they discover how
Python treats default arguments in function definitions.

Let's say you want to define a function that accepts a list as a parameter, and you
want the default value of that list to be the empty list, so you write:

```python
def append_to(element, to=[]):
    to.append(element)
    return to
```

If everything was okay, you would expect the following behavior:

```
my_list = append_to(12)
print my_list

my_other_list = append_to(42)
print my_other_list
```

```
[12]
[42]
```

But what you get instead is:

```
[12]
[12, 42]
```

A new list is created once when the function is defined, and the same list is used in each successive call.

Python’s default arguments are evaluated once when the function is defined, instead of each time the function is called (like it is in say Ruby). This means that if you use a mutable default argument and mutate it, you will and have mutated that object for all future calls to the function as well.

### What you should do
Create a new object each time the function is called, by using a default arg to signal that no argument was provided (`None` is often a good choice):

```python
def append_to(element, to=None):
    if to is None:
        to = []
    to.append(element)
    return to
```