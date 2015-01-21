# Getting all but the first element from Ruby array

When getting all but the first element from an array in Ruby, we have a few
options.

Given the following list:

```ruby
list = [1,2,3,4]
```

## Shift

We could use [`shift`][shift docs], however it mutates the array. It also
doesn't return the list so we need two lines to write this code:

```ruby
list.shift
# => 1
rest_of_list = list
# => [2,3,4]
```

## Slice

In the past I've used [`slice`][slice docs], but specifying indices or passing
the length of an array is ugly and low-level:

```ruby
rest_of_list = list[1..-1]
# => [2,3,4]
rest_of_list = list.slice(1, list.length)
# => [2,3,4]

list # is not modified
# => [1,2,3,4]
```

## Drop

My new favorite is [`drop`][drop docs] which does not mutate and does not
require ugly, low-level code:

```ruby
list.drop(1)
# => [2,3,4]

list # is not modified
# => [1,2,3,4]
```

An added benefit of`drop` is that it will always return an array, while `slice`
will sometimes return `nil`

```ruby
[].slice(1..-1)
# => nil

[].drop(1)
# => []
```

[shift docs]: http://www.ruby-doc.org/core-2.2.0/Array.html#method-i-shift
[slice docs]: http://www.ruby-doc.org/core-2.2.0/Array.html#method-i-slice
[drop docs]: http://www.ruby-doc.org/core-2.2.0/Array.html#method-i-drop
