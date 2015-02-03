# Constant time comparison

Using `==` to compare sensitive hashes leaves you vulnerable to timing attacks.
This is because `==` returns `false` as soon as it finds two characters that
don't match. An attacker can make many requests with different values and
compare times to figure out how many characters were correct (the shorter the
response, the fewer correct characters).

The solution to this problem is to use a constant-time comparison algorithm.
This ensures that the method will always take the same amount of time,
regardless of how similar the hashes are. In Ruby, you can use
[`Rack::Utils.secure_compare`] or
[`ActiveSupport::SecurityUtils.secure_compare`].

For more information, check out this excellent [blog post].

[`Rack::Utils.secure_compare`]:
http://www.rubydoc.info/github/rack/rack/Rack/Utils#secure_compare-class_method
[`ActiveSupport::SecurityUtils.secure_compare`]:
http://api.rubyonrails.org/classes/ActiveSupport/SecurityUtils.html#method-c-secure_compare
[blog post]: http://codahale.com/a-lesson-in-timing-attacks/
