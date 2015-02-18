# Using pry and ncurses together

Because of ncurse's visual mode you will not be able to use pry normally.
The easiest way to get pry working is to do the following:

```ruby
close_screen
binding.pry
refresh
```

[`close\_screen`][close_screen docs] restores the non-visual mode which allows you to see the
output of pry correctly. When you `exit` from pry, `refresh` will resume
ncurse's visual mode.

[last docs]: (http://ruby-doc.org/stdlib-2.0/libdoc/curses/rdoc/Curses.html#method-c-close_screen)
