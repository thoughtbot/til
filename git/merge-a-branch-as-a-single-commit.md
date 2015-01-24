# Merge all changes from another branch as a single commit:

Let's say you want to merge "my-feature" (which contain 10 commits :D ) into develop:

    git checkout develop
    git merge --squash my-feature
    git commit -m "Merging my-feature branch"

Now instead of adding all "my-feature" commits to develop we added them all as a single commit.

###### I don't recommand using this always but sometimes it's useful to keep history clean.
