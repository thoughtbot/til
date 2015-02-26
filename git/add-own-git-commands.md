# Adding your own git commands

Git uses a simple schema for all its commands. Any executable in your
$PATH named git-foo, will be reachable via `git foo` from the
commandline.

For example, here is a command to extend the last commit without modifying the commit comment. It's like a dwim amend for 90% of the cases.

```bash
git commit --amend --no-edit
```

put it in your path, and you'll be able to call it with a simple `git
extend`.

# Adding it to zsh's autocompletion system

Add this to your .zshrc to make every git-* file in your path available as a completion to git.

``` zsh
zstyle ':completion:*:*:git:*' user-commands ${${(M)${(k)commands}:#git-*}/git-/}
```
