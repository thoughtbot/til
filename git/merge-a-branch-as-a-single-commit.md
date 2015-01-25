# Merge all changes from another branch as a single commit:

Let's say you want to merge "my-feature" (which contain 10 commits :D ) into develop:

    git checkout develop
    git merge --squash my-feature // Will stage new files for commit.
    git commit -m "Merging my-feature branch"
