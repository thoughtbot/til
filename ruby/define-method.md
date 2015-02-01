# Method Definition

MRI Ruby provides syntax `def` that allow you to define a method.

```ruby
def my_method
end

# => :my_method
```

The returned value of a method definition is the symbol naming of the method. This is useful when you want to define and parse the method naming at the same time into other method. For example, you could expose helper method in Rails controller like this:

```ruby
def MyController < ActionController::Base
  helper_method def my_helper
                  # my_code
                end
end
```

Besides, it is also possible to define new instance method dynamically by taking advantage of metaprogramming techniques in Ruby with `define_method`. This method takes in a Proc, a Method or an UnboundMethod object. If a block is given, it will be used as the body of the method and will be evalulated with `instance_eval`. Example:

```ruby
class MyObject
  define_method(:hello) { puts "Hello" }
end

MyObject.new.hello
# => Hello
```

