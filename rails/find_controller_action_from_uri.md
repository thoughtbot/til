# Find a controller and action from a URI string

Got `GET /posts`, want to craft a `redirect_to` based off of that URI and some other parameters?

Today I learned that you can extract out the controller and action for a particular route with the magical
`ActionDispatch::Routing::RouteSet#recognize_path`,
which can be called through `Rails.application.routes.recognize_path`.

**Warning**: `#recognize_path` isn't part of Rails' user facing public API.
Do **not** use in production - its behavior might change without notice.

So given a routes file:

```ruby
# config/routes.rb
# ...
resources :posts
# ...
```
And jumping into the rails console:
```bash
$ bundle exec rails console
```
Try out the following:
```ruby
Rails.application.routes.recognize_path('/posts') #=> { controller: 'posts', action: 'index' }
```

I used it working on authorization system. I needed to disable links that user has no access to follow. In my controller I have defined two arrays: read actions and manage actions. So creating link I checked user permissions and permissions needed to follow the link.

Nevertheless, I think `#recognize_path` is an interesting, undocumented, and [huge][4_1_8_recognize_path_source] part `ActionDispatch::Routing::RouteSet`'s API!

[4_1_8_recognize_path_source]:https://github.com/rails/rails/blob/v4.1.8/actionpack/lib/action_dispatch/routing/route_set.rb#L681-L719
