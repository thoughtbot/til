# Currying in Ruby

Ruby defines `curry` for `Method` and `Proc`, allowing procs to return partially
applied procs when they get called with fewer than the required number of
arguments. For example:

```ruby
multiply = -> x,y { x * y }.curry
#=> #<Proc:0x007fed33851510 (lambda)>
multiply[2,3]
#=> 6
double = multiply[2]
#=> #<Proc:0x007fed35892888 (lambda)>
double[3]
#=> 6
```

**Note:** While `Proc#curry` has been around since Ruby 1.9, `Method#curry` was
only added in Ruby 2.2.0. For versions before 2.2.0, you will first need to
convert your method object to a proc via `Method#to_proc`.

Check out the [Ruby docs] for more details.

[Ruby docs]: http://ruby-doc.org/core-2.2.0/Proc.html#method-i-curry
