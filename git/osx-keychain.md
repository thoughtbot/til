# Using git's osxkeychain helper to cache GitHub authentication

Recently after reformatting my computer I've had to input my username/password
every time I try to do something with GitHub via the command line. Today I took
the time to finally figure out what was going on.

Turns out that I had a newer version of git that behaves a little differently.
Today I learned that you need to configure git to use this so it will stop
nagging you.

## The Symptoms

1. You are asked for your username and password when you interact with
   an HTTPS GitHub remote.
2. It does not ask for your username and password when you interact with an SSH
   GitHub remote.
3. Your git version is 1.7.10 or newer. Run `git --version` to find out which
   version you have.

## The Cure

You need to configure git to cache your username and password with the
osxkeychain credential helper.

GitHub's help pages describe how to do this [here](https://help.github.com/articles/caching-your-github-password-in-git/)

