# Enumerable tricks

## Enumerable#each_cons

Sometimes you need to compare a value in an array with the previous
value, the next value, or both. [`Enumerable#each_cons`][each_cons docs] to the rescue!

```ruby
(1..10).each_cons(3) { |element| p element }

# outputs below
[1, 2, 3]
[2, 3, 4]
[3, 4, 5]
[4, 5, 6]
[5, 6, 7]
[6, 7, 8]
[7, 8, 9]
[8, 9, 10]
```

[each_cons docs]: http://ruby-doc.org/core-2.2.0/Enumerable.html#method-i-each_cons

