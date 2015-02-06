# Two ways of squashing commits

It is handy to squash down your commits before merging your PR with
`my-new-cool-feature`. You can either squash them down by doing an interactive
rebase like so:

```bash
$ git checkout my-new-cool-feature
$ git rebase -i master
```

This will open up your `$EDITOR` of choice and you are free to pick and choose
which commits to squash together.

This might be tedious if you have a big number of commits to squash together.
Very tedious. TIL that you can use `git merge` to squash your commits, all in
one go.

```bash
$ git checkout master
$ git merge --squash my-cool-new-feature
```

This will leave all of your changes staged on `master`, ready to be committed as
one.
