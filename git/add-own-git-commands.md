# Adding your own git commands

Git uses a simple schema for all its commands. Any executable in your
`$PATH` named git-foo, will be reachable via `git foo` from the
commandline.

For example, here is a command to extend the last commit without
modifying the commit comment. It's like a dwim amend for 90% of the
cases. Save it as git-extend somewhere in your `$PATH`.

```bash
git commit --amend --no-edit
```

Now, you'll be able to call it with a simple `git extend` from the
command line.

# Adding it to zsh's autocompletion system

Add this to your .zshrc to make every git-* file in your path
available as a completion to git.

``` zsh
zstyle ':completion:*:*:git:*' user-commands ${${(M)${(k)commands}:#git-*}/git-/}
```
