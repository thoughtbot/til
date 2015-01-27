# Returning a fixed amount of items from the tail of a list

[`Array#last`][last docs] takes an argument to limit the number of items to return 
from the tail of a list.

```ruby
> [1,2,3,4,5].last(2)
# = > [4, 5]
```

[last docs](http://www.ruby-doc.org/core-2.2.0/Array.html#method-i-last)
