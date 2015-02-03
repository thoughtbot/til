`Rack::Test` defaults to URL Encoding Parameters
================================================

By default, Rack's test helpers set the `Content-Type` header to
`application/x-www-form-urlencoded`.

The URL encoded representation of

```json
{ "tags": ["foo", "bar"] }
```

would be

```
?tags[]=foo&tags[]=bar
```

This works as expected for non-empty arrays:

```ruby
put "/api/v1/post/1", {
  post: { tags: ["foo"] }
}
```

However, it isn't possible to represent `[]` as a URL encoded string.

```ruby
put "/api/v1/post/1", {
  post: { tags: [] }
}
```

would be invalidly encoded as:

```
?tags[]=
```

As a result, Rack ignores the `tags` key, which would make the `post` key point
to an empty hash, which Rack also ignores.

To work around this issue:

* transform the `params` hash to a [`JSON` string][rack-test]
* append `.json` to the URL
* explicitly set the `"Content-Type"` header to `"application/json"`

```ruby
put "/api/v1/post/1.json", {
  post: { tags: [] }
}.to_json, { "Content-Type" => "application.json" }
```

This pattern can be extracted to a helper:

```ruby
def json_put(path, params, headers_or_env = {})
  json_path = "#{path}.json"
  params_without_format = params.except(:format)
  headers = headers_or_env.reverse_merge("Content-Type" => "application/json")

  put(json_path, params_without_format.to_json, headers)
end


json_put "/api/v1/post/1", {
  post: { tags: [] }
}
```

Coincidentally, Basecamp has a similar set of test helpers.

[rack-test]: https://github.com/brynary/rack-test/blob/acdbee66fc765f15c2d3a1a372c368fe8ee0a49c/lib/rack/test.rb#L218-L228
