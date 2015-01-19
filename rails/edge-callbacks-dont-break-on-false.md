# Callbacks in Edge Rails

In Edge Rails, callbacks won't stop if you return `false`, you need to throw
`:abort` . This prevents really subtle bugs where a method in a callback returns
`false`, unintentionally breaking the callback chain. For example, the following
would previously have halted the callback chain:

```ruby
def unset_admin
  self.admin = false
end
```

Check out the [pull request] on Rails to see the discussion around this feature.

**Note:** This feature is currently slated be included as part of the Rails 5
release.

[pull request]: https://github.com/rails/rails/pull/17227
