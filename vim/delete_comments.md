# Delete all comments in one go

Every Rails app you generate comes with many files such as routes that includes lots of comments.

You can delete all these comments at once using the following vim command:

```vimscript
:g:^#:normal dd
```