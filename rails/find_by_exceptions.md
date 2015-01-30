## Exceptions Raised by `find_by` vs. `find`

I previously believed that the following were the same - the former being the more concise, and by extension making the latter overly verbose:

```ruby
ObjectModel.find(3) # good
ObjectModel.find_by(id: 3) # bad?
```

Today, one of my teammates ([@dleve123](https://github.com/dleve123)) pushed up a PR with the latter line. One of the finer points of `find_by` is that attempting to retrieve an id that doesn't exist will simply return `nil`. I now understand that the following is more accurate:

```ruby
ObjectModel.find(3) # good
ObjectModel.find_by!(id: 3) # bad!

ObjectModel.find_by(id: 3) # good, when trying to avoid exceptions
```

`find_by!` will raise an exception and makes the first two essentially the same. It should be noted that the dynamic `find_by_[attribute]` methods follow the same convention, though they are [mildly deprecated](http://api.rubyonrails.org/classes/ActiveRecord/Base.html#class-ActiveRecord::Base-label-Dynamic+attribute-based+finders). This also extends to all other uses of the `find_by` with attributes other than `id`:


```ruby
ObjectModel.find_by!(name: "foo") # use when exceptions should be raised
ObjectModel.find_by(name: "foo")  # use when exceptions should be surpressed
```
