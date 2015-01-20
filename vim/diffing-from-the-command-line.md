# Easy file diffing

Vim comes with its own diff viewer. It can be launched from the command-line
with:

```bash
vim -d file1 file2
# or
vimdiff file1 file2
```

You can also get a diff from within Vim by opening two files in
splits and running `:diffthis`.

More details in `:help vimdiff`, or check out the [online docs].

[online docs]: http://vimdoc.sourceforge.net/htmldoc/diff.html#vimdiff
