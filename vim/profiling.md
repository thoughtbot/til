# Vim Profiling

I recently encountered a situation where Vim was taking an *excruciatingly* long
time to launch. From some manual testing, I was able to isolate the problem to a
particular directory, but I wasn't sure what was causing it. I then discovered
Vim ships with profiling tools that would tell me how much time was spent in
each of the functions that ran during startup. See the [official docs] for more
info.

I'll start with the shell command I ended up running:

```sh
vim -c 'profile start vim.log' -c 'profile func *' -c 'e config/routes.rb' -c 'q'
```

The `-c` option tells Vim to execute the given command after loading the first
file (in this case the empty buffer), and will execute multiple `-c` options
sequentially.

To break it down:

* `-c 'profile start vim.log'` starts the profiler, logging results to the
  vim.log file.
* `-c 'profile func *'` enables profiling of functions matching the given
  pattern. All functions, in this case.
* `-c 'e config/routes.rb'` opens the routes file. This was arbitrary for my
  purposes, as opening any file in the Rails application was slow.
* `-c 'q'` quits.

The `vim.log` file has a lot of detail about the functions that were executed.
Here's a short one that was near the top for me.

```text
FUNCTION  fugitive#is_git_dir()
Called 18 times
Total time:   0.000396
 Self time:   0.000233

count  total (s)   self (s)
   18   0.000271   0.000108   let path = s:sub(a:path, '[\/]$', '') . '/'
   18              0.000107   return isdirectory(path.'objects') && isdirectory(path.'refs') && getfsize(path.'HEAD') > 10

```

That's interesting, for sure, but the good stuff is at the bottom of the file,
where functions are sorted by execution time. Here's my top offender.

```text
count  total (s)   self (s)  function
    1   2.203751   0.000457  rails#buffer_syntax()
```

[official docs]: http://vimdoc.sourceforge.net/htmldoc/repeat.html#profiling
