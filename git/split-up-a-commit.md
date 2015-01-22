# Split Up a Commit, Rewrite History

When working on a branch with multiple commits, you can "go back in time" and revise previous commits any way you please.

    $ git rebase -i origin/master

This command will prompt you inside of your `$VISUAL` with a series of commit SHAs and commit titles

    # ...
    pick ed1ff41 Move templates
    pick 274ac0e Move components & views
    # ...

To split up `274ac0e`, replace `pick` with `edit` and save the buffer.

    # ...
    pick ed1ff41 Move templates
    edit 274ac0e Move components & views
    # ...

You are now detached from the `HEAD` of your branch and "back in time".
To split up the current commit (`274ac0e`):

    $ git reset HEAD~

This will unstage all files within the commit.
Next, split up the commit any way you'd like.

    $ git add app/views
    $ git commit -m "Move views"
    $ git add app/components
    $ git commit -m "Move components"

When you're finished, continue the rebase.

    $ git rebase --continue

If you introduced merge conflicts down the line, you'll have to resolve them.
If all went well, your branch's history will be re-written.

    $ git log origin/master..

    # ...
    ed1ff41 Move templates
    7b84a01 Move views
    274ac0e Move components
    # ...

Keep in mind that you might have to force push your branch to `origin`,
depending on whether or not your revised commits have been pushed.

    $ git push origin my-branch-name --force
