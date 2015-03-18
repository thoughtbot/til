# Inject vs each_with_object

## Inject

Inject takes the value of the block and passes it along.
This causes a lot of errors like.

```ruby
  inject_array = ['A', 'B', 'C', 'D']

  inject_array.inject({}) do |accumulator, value|
    accumulator[value] = value.downcase
  end
  
  Output: 'IndexError: string not matched'
```

The above code causes 'IndexError: string not matched' error.

What you really wanted.

```ruby
  inject_array = ['A', 'B', 'C', 'D']

  inject_array.inject({}) do |accumulator, value|
    accumulator[value] = value.downcase
    accumulator
  end

  Output: => {"A"=>"a", "B"=>"b", "C"=>"c", "D"=>"d"}
  ```

## each_with_object

  each_with_object ignores the return value of the block and passes the initial object along.

```ruby
  array = ['A', 'B', 'C', 'D']

  array.each_with_object({}) do |value, accumulator|
    accumulator[value] = value.downcase
  end

  Output: => {"A"=>"a", "B"=>"b", "C"=>"c", "D"=>"d"}
  ```
One more thing which you can notice is the order of arguments to the block for each of the functions.

Inject takes the result/accumulator and then the iteratable value, whereas 'each_with_object' takes the value followed by the result/accumulator.
