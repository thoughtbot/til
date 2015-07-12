# `.strip_heredoc`

Heredocs are quite useful for using longer segments of text or code in a file:

```ruby
def content
  <<-HTML
  <p>Content of the blog post</p>
  <a href="http://example.com">A link</a>
  HTML
end
```

However, since heredocs treat all the text literally, the indents remain:

```html
"  <p>Content of the blog post</p>\n  <a href=\"http://example.com\">A link</a>\n"
```

Notice the extra space at the start and before the link tag. One solution is to outdent the code:

```ruby
def content
  <<-HTML
<p>Content of the blog post</p>
<a href="http://example.com">A link</a>
HTML
end
```

But that looks pretty ugly. Rails provides a method called `.strip_heredoc` on String that does this for us:

```ruby
def content
  <<-HTML.strip_heredoc
  <p>Content of the blog post</p>
  <a href="http://example.com">A link</a>
  HTML
end
```

```html
"<p>Content of the blog post</p>\n<a href=\"http://example.com\">A link</a>\n"
```

Nice and clean.

If you need to load this outside of rails:

```ruby
require 'active_support/core_ext/string/strip'
```
