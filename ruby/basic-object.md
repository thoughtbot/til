# Basic Object

Ruby has a `BasicObject` class which doesn't include Kernel methods.

This is useful for delegators which would otherwise not delegate methods such as
\#to_s.

Example:

```ruby
class ListDelegator < BasicObject
  def initialize(*list)
    @list = list
  end

  def method_missing(method, *args, &block)
    @list.map do |item|
      item.__send__(method, *args, &block)
    end
  end
end

class Out
  def to_s
    "Out"
  end
end

ListDelegator.new(Out.new).to_s # => ["Out"]
```


