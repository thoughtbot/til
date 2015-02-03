# Man Section 7

For most of us, `man` pages are primarily the source of documentation for various system-level tools, be it `curl`, `ssh`, `gcc` or multitude of others.

But that's not all that there is. TIL about `man` section 7 and some of its pages that you can't visit by mere accident.

As `man 7 intro` puts it:

```
intro - Introduction to overview, conventions, and miscellany section

Section  7  of  the  manual  provides  overviews  on  various  topics, and
describes conventions and protocols, character set standards, the standard
file system layout, and miscellaneous other things.
```

You can see the entire list for yourself with one of the following commands, depending on your system:

```
apropos '.*' | grep '(7.* - ' | sort | less
```

or

```
apropos sec=7 | sort | less
```

or

```
ls -1 /usr/share/man/man7 | sed 's:\.7.*\.gz$::' | xargs whatis | less
```

Here is the overview of some pages that stood out to me. To visit a page, type `man <name>` or `man 7 <name>` to avoid collisions with pages in other sections.

*Note: you can lack some pages from the list below on your system.*

| page            | description
| :-------------: | :----------
| ascii           | ASCII table right in your `man` pager. With no extra tools. In 3 different layouts!
| boot            | Fantastic and rather condensed explanation of Linux boot sequence.
| charsets        | "Programmer's view" of different character sets, including ASCII, ISO 8859 (Latin-x), Unicode and some lesser known national charsets. Hopefully not particularly relevant anymore.
| complex         | Basics of complex number arithmetics, as a `man` page!
| credentials     | PID, PPID, GID, SID, UID.
| des_modes       | Cryptographic modes for block cyphers (ECB, CBC and others). Not specific to DES at all! Although the page leaves much to be desired.
| fifo            | Awesome named pipes!
| fsf-funding     | Some info about ways to support free software development (not only FSF). Too focused on encouraging redistributors to donate IMO, but still interesting.
| glob            | Unix globbing rules.
| gpl             | GNU General Public License.
| hier            | Description of the file system hierarchy! Ever wondered what `/usr/share` really means?
| mailaddr        | Email address description, in case you forgot.
| man-pages       | Conventions for writing `man` pages. Probably useful on its own, as a source of advice for writing any kind of technical documentation.
| operator        | Operator precedence of the C language! Don't google it anymore, you have this useful `man` page preinstalled.
| path_resolution | Detailed overview of path resolution process. Absolute vs. relative, permissions, symlinks, mount points, trailing slash.
| pipes           | Pipes and FIFOs.
| regex           | POSIX.2 regular expressions syntax.
| signal          | All you need to know about the signals.
| suffixes        | Outdated list of file extensions. Might be useful some day.
| symlink         | Symlinks and hardlinks in detail.
| time            | Time in Unix.
| unicode         | Unicode.
| units           | SI unit prefixes! Both decimal (from yocto to yotta) and binary (up to exbi).
| uri             | URLs and URNs, with BNF, examples, percent encoding and other notes!
| utf8            | More details on UTF-8 encoding.

These I guess came with Git, but nonetheless:

| page             | description
| :--------------: | :----------
| gitglossary      | Comprehensive glossary of GIT terms, such as "octopus", "porcelain", "evil merge", and others.
| gittutorial      | Tutorial covering the first steps in using Git.
| gittutorial-2    | More advanced aspects of Git: object database and the index file.
| gitcore-tutorial | Yet another tutorial which explains stuff on a lower level. It's huge.
| gitworkflows     | Overview of recommended workflows with Git.
