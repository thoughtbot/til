# Bad JS path triggers CSRF/CORS exception

Rails v4.1.6

If a controller uses [`protect_from_forgery`](http://guides.rubyonrails.org/security.html#csrf-countermeasures),
rendering a view with an incorrect JS path can trigger

    Failure/Error: Unable to find matching line from backtrace
    ActionController::InvalidCrossOriginRequest:
      Security warning: an embedded <script> tag on another site requested
      protected JavaScript. If you know what you're doing, go ahead and
      disable forgery protection on this action to permit cross-origin
      JavaScript embedding.

under `test` &mdash; though not for the reason shown in the [RailsGuide]
(http://guides.rubyonrails.org/upgrading_ruby_on_rails.html#csrf-protection-from-remote-script-tags).

In my case, the project seemed to work in `development`, but my new Capybara
`feature` spec triggered the exception.

I found a weeks-old commit that had moved/renamed

    app/assets/javascripts/create_a_class.js

to

    app/assets/javascripts/scorebook/create_a_class.js

Changing the view's

```erb
<%= javascript_include_tag 'create_a_class.js' %>
```

to

```erb
<%= javascript_include_tag 'scorebook/create_a_class.js' %>
```

fixed the exception.
