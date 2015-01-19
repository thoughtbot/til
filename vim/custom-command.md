# Custom commands

Custom commands in Vim are defined via the `command` command. As I learn new
things throughout the week, I like to write them down in a `TIL.md` file. I
found myself constantly running `:tabe ~/Documents/TIL.md` to open my file in a
new tab. To streamline the process, I added the following to my `.vimrc`:

```vimscript
command TIL tabe~/Document/TIL.md
```

Now, whenever I want to write down something I've learned I can just run `:TIL`.

User-defined commands _must_ start with a uppercase letter.

More details in `:help command`, or check out the [online vim docs].

[online vim docs]: http://vimdoc.sourceforge.net/htmldoc/map.html#:command
