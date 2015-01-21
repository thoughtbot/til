# Capybara `all` does not return an array

Although it looks like it returns an `Array`, Capybara's `all` finder actually
returns a `Capybara::Result`. This object includes `Enumerable` and responds to
many of the most used methods on `Array` such as `[]`.

Given the following HTML:

```ruby
<body>
  <p>Some content</p>
  <p>Other content</p>
  <p>Final content</p>
</body>
```

The following really looks like we are dealing with an array:

```ruby
paragraphs = all("p")
# => [<Capybara::Element>,<Capybara::Element>,<Capybara::Element>]

paragraphs[1]
# => <Capybara::Element>

paragraphs.map(&:text)
# => ["Some content", "Other content", "Final Content"]
```

However, if I try to use some of the `Array` monkey patches provided by
`ActiveSupport`:

```ruby
paragraphs.second
# => NoMethodError: undefined method `second' for Capybara::Result

paragraphs.class
# => Capybara::Result
```
