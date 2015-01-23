# Replace if/else conditionals with guard clauses

When doing a lot of nested conditionals you may end facing a code like this:

```ruby
def result_with_nested_conditionals
  if condition_one
    return result_one
  elsif condition_two
    return result_two
  else
    return result_three
  end
end
```

As you can see, this is a unreadable piece of code and could be worse if we add some new levels of conditions.

Using Guard clauses will make your code more readable:

```ruby
def result_with_guard_clauses
  return result_one if condition_one
  return result_two if condition_two
  return result_three
end
```
