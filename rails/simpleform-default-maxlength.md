# Inferred `maxlength` in Simple Form

The [Simple Form gem] gives us some advanced features built on top of Rails'
form builder. One such feature is the ability to infer the `maxlength` attribute
by reading the validations on an `ActiveRecord` model. This can be set by
opening the simple form initializer and changing `b.optional :maxlength` to
`b.use :maxlength`. This file is well documented with comments.

```ruby
# config/initializers/simple_form.rb

SimpleForm.setup do |config|
  config.wrappers :default, :class: input,
    hint_class: :field_with_hint, error_class: :field_with_errors do

    ## Optional extensions
    # They are disabled unless you pass `f.input EXTENSION_NAME => true`
    # to the input. If so, they will retrieve the values from the model
    # if any exists. If you want to enable any of those
    # extensions by default, you can change `b.optional` to `b.use`.

    # Calculates maxlength from length validations for string inputs
    b.optional :maxlength
  end
end
```

[Simple Form gem]: https://github.com/plataformatec/simple_form
