# Search & Replace in multiple files

I recently had to replace static files path in multiple files from a project
I were working on, after boggling my mind trying to do it with
[sed](http://en.wikipedia.org/wiki/Sed), I gave up and looked up how to do it
using VIM, I was sure there was a way.

When VIM is started, you can specify multiple files to open as buffers from the
terminal:

```bash
vim *.html
```

This will open all html files on the current directory as buffers.
* You can list the buffers using `:ls`
* You can add a buffer using `:badd <filename>`
* You can close a buffer using `:bdelete <buffer_number>`

Now you can run commands on all open buffers:

```vimscript
:bufdo <command>
```

Searching all instances of **foo** and replacing with **bar**:

```vimscript
:bufdo %s/foo/bar/ge
```

**Notice**: the **e** on the replace command tells vim to ignore errors,
otherwise vim would print an error on each file that doesn't have a match for
**foo**

You can now open the buffers (`:buffer <buffer_number>`) and verify that the
text was replaced.

But this command only replaced the text, we need to save the files to persist
changes:

You can either run another **bufdo** with the **update** command to save the
files:

```vimscript
:bufdo update
```

Or you can pipe it on the first command:

```vimscript
:bufdo %s/foo/bar/g | update
```

And that's it!
