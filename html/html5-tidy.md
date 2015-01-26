# Tidy with HTML5 support

There is a tool called `tidy` which was originally written by [Dave
Raggett][tidy] (in the late '90s), and is now [maintained by
volunteers][tidy-sf] and the W3C.

There is an experimental fork of `tidy` which is maintained by the HTML Tidy
Advocacy Community Group which supports the modern HTML5 spec.

This tool takes HTML/XML/XHTML as input and produces a valid version as its
output. It also accepts flags which make it more useful as an error-checking
lint tool, and does not re-write files. Example usage of `tidy`:

`find tmp -name "*.html" -print -exec tidy -qe {} \;`

Here's what's happening:

* Run the `find` tool, tell find to look in the `tmp/` directory, and locate all
  files with an `html` file extension.
* Tell `find` to print out the names of every file.
* Tell `find` to execute a process and send the output (all the html file names)
  to that process.
* Use `tidy` with options of `q` (quiet mode) and `e` (only show errors).

The resulting output contains a list of all files in `tmp/`, along with any
errors in the HTML of those files.

[tidy]: http://www.w3.org/People/Raggett/tidy/
[tidy-sf]: http://tidy.sourceforge.net/
[experiment-html5]: http://www.htacg.org/tidy-html5/
