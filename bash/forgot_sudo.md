## Forgot to write `sudo` before your command? No problem !!

You can write `sudo !!` immediately after your last command.
#### Example 1

```bash
$ sudo apache2 status
Absolute path to 'service' is '/usr/sbin/service', 
so running it may require superuser privileges (eg. root).
$ sudo !!
sudo service apache2 status
```

### Turn it into an alias

`!!` can be expanded to `$(history -p !!)` and turned to an alias that you can add to your `~/.bashrc`
```bash
alias whoops='sudo $(history -p !!)'
```
#### Example 2

```bash
$ sudo apache2 status
Absolute path to 'service' is '/usr/sbin/service', 
so running it may require superuser privileges (eg. root).
$ whoops
sudo service apache2 status
```
