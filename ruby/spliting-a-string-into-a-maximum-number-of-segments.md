# Spliting a string into a maximum number of segments

[`String#split`][split docs] takes an argument to limit the number of returned
matches. Once the limit is reached, the rest of the string is returned as one
match even if it contains more delimiters.

For example, say we are parsing a string whose first two lines are always
headers and the rest is the body:

```ruby
text = <<-TEXT
header1 = value
header2 = value
the body
keeps going
on over
multiple lines
TEXT
```

A simple `split` on newlines would create an array with each line as an
individual element:

```ruby
text.split("\n")
# => ["header1 = value",
#     "header2 = value",
#     "the body",
#     "keeps going",
#     "on over",
#     "multiple lines"]
```

Since we know there are two headers and a body, we can tell `split` to stop
splitting once we have three segments:

```ruby
text.split("\n", 3)
# => ["header1 = value",
#     "header2 = value",
#     "the body\nkeeps going\non over\nmultiple lines"]
```

[split docs]: http://www.ruby-doc.org/core-2.2.0/String.html#method-i-split
