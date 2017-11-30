# Use a file from another branch

Sometimes you just need one file from another branch. Sure you could `git
cherry-pick` but then you're dealing with commits. That sort of thing gets
sticky fast; don't go there.

The best way is to use your old pal `git checkout`. Just make sure you're
on the branch you want to bring the file into and then checkout the file
from its source branch. Here's the syntax.

```
$ git checkout my-awesome-source-branch the/path/to/yourfile.rad
```

That's it – enjoy.
