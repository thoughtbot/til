# Accessing route helpers in the console

If you're working on a more complex route, it's great to make sure your path helpers work.
Often, this involves sticking the helper in a controller or view to try it out, which can be tedious.
The Rails console offers a quick helper to check route paths: the `app` method.

Assuming you have something like `resources :users` in your routes file:

```ruby
app.users_path
# => "/users"
app.user_path(1)
# => "/users/1"
```

Updating your routes file to have `resources :posts` instead, and reloading the console:

```ruby
reload!
app.posts_path
# => "/posts"
```

This lets you have a tight feedback loop when working on your routes.
