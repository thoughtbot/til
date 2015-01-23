# Parallel assignment

Ruby allows us to assign multiple variables on the same line. This is also
called parallel assignment.

```ruby
a, b = 1, 2
#=> [1, 2]
a
#=> 1
b
#=> 2
```

We can also use parallel assignment and the splat operator in combination to
split the array into the head and tail. This is in particular useful if we want
to [get all but the first element from an array](all-but-the-first-element-from-array.md).

```ruby
list = [1,2,3,4]
#=> [1,2,3,4]
head, *tail = list
#=> [1,2,3,4]
head
#=> 1
tail
#=> [2,3,4]

list # is not modified
#=> [1,2,3,4]
```

### Empty arrays
When using parallel assignment on an empty array, the tail will always return an
array while the head will be `nil`.

```ruby
head, *tail = []
#=> []
head
#=> nil
tail
#=> []
```
