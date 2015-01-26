# The `DATA` constant

The `DATA` constant in Ruby allows us to access the text at the end of our file
listed after the `__END__` block. This can be surprisingly useful, for instance
if we need to extract information from a rather large data blob.

Imagine a scenario where we need to extract the user names from a SQL statement.

```ruby
puts DATA.read.gsub("ALTER USER ", "").gsub(/IDENTIFIED BY.+/, "")

__END__
ALTER USER Annette IDENTIFIED BY 'Annette';
ALTER USER Warren IDENTIFIED BY 'Warren';
ALTER USER Anthony IDENTIFIED BY 'Anthony ';
ALTER USER Preston IDENTIFIED BY 'Preston';
ALTER USER Kelly IDENTIFIED BY 'Kelly ';
ALTER USER Taylor IDENTIFIED BY 'Taylor';
ALTER USER Stiller IDENTIFIED BY 'Stiller';
ALTER USER Dennis IDENTIFIED BY 'Dennis';
ALTER USER Schwart IDENTIFIED BY 'Schwart';
```

Executing the file will print this:

```
Annette
Warren
Anthony
Preston
Kelly
Taylor
Stiller
Dennis
Schwart
```

Since `DATA` is simply just a virtual `File` object within our file, we can also
pass the `DATA` variable (without `#read`) to methods that accept a `File`.

```ruby
require "json"

puts JSON.load(DATA)

__END__
{
  "records": [
    {
      "artist":"Iggy Pop",
      "title":"Lust for Life"
    },
    {
      "artist":"Television",
      "title":"Marquee Moon"
    },
    {
      "artist":"Talking Heads",
      "title":"Talking Heads: 77"
    }
  ]
}
```
