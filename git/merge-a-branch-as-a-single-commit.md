# Merge all changes from another branch as a single commit:

Let's say you want to merge `another-branch` (which contains 10 commits) into `master`:

    git checkout master
    git merge --squash another-branch #Will stage new files for commit.
    git commit
