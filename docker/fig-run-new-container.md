# `fig run` Runs Commands on New Containers

In a project I've been working on that deploys with [Docker] and [Fig], we're
using [Ragel] and [Racc] to build a parser and lexer; the Ruby files are
generated and written to the filesystem with a rake task when running `fig up
web`.

[docker]: https://www.docker.com/
[fig]: http://www.fig.sh/
[ragel]: http://www.colm.net/open-source/ragel/
[racc]: https://github.com/tenderlove/racc

However, running `fig run web rails c` was demonstrating weird behavior; the
parser and lexer constants weren't defined in Ruby, and they weren't present
on the filesystem either.

After a bit of digging through [fig's CLI documentation][fig-cli], I found
that `fig run` brings up new containers to manage one-off commands instead of
connecting to the same running container. This means any changes to the
filesystem (like generating a parser and lexer, or more commonly log files or
compiled assets) are not available during `fig run`.

[fig-cli]: http://www.fig.sh/cli.html
