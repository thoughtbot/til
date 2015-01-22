# Basic Object

Ruby has a `BasicObject` class which doesn't include Kernel methods and acts as
the parent for all `Object`s. You can see the ancestry in practice via:

```ruby
Object.ancestors # => [Object, Kernel, BasicObject]
BasicObject.ancestors # => [BasicObject]
```

`BasicObject` thus has very few instance methods which would be inherited by a
subclass:

```ruby
BasicObject.instance_methods # => [:==, :equal?, :!, :!=, :instance_eval, :instance_exec, :__send__, :__id__]
Object.instance_methods.length # => 55
```

This is useful for delegators which would otherwise not delegate methods such as
\#to_s.

Example:

```ruby
class ListDelegator
  def initialize(*list)
    @list = list
  end

  def method_missing(method, *args, &block)
    @list.map do |item|
      item.__send__(method, *args, &block)
    end
  end
end

class ListDelegatorBasic < BasicObject
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

ListDelegator.new(Out.new).to_s # => "#<ListDelegator2:0x007fcab400d148>"
ListDelegatorBasic.new(Out.new).to_s # => ["Out"]
```
