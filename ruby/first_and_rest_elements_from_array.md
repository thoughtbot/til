# Getting first element and rest of elements from Ruby array

```ruby
first, *rest = *zero
first                           # => nil
rest                            # => []
first, *rest = *one
first                           # => 0
rest                            # => []
first, *rest = *many
first                           # => 0
rest                            # => [1, 2, 3, 4]
```

|> via http://devblog.avdi.org/2010/01/31/first-and-rest-in-ruby/
