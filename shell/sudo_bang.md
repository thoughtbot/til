# Useful *Bang*

I found another great thing bash console provides for the lazy programmers. Most of the time we need to repeat the commands we entered in shell and many hardworking engineers typing it again and again.

Shell provides many tools which remembers history and on top of that we can make our life easy.

Usually i work on servers and whenever try to fire few root access commands and it dont allow me!!, feels insulting. Anyway _Bang_ commands make it easy to re-run commands as root if you forget to use sudo.

more can be found at:

+ http://ss64.com/bash/history.html
+ http://codeinventory.com/linux/2014/09/14/bang-bang/

![Bang-bang](http://codeinventory.com/images/bang-bang.jpg)

```
amey@amey-xps:~/$ touch /etc/apache2/apache2.conf 
touch: cannot touch ‘/etc/apache2/apache2.conf’: Permission denied

amey@amey-xps:~/work/blog/codeinventory.github.io/_posts$ sudo !!
sudo touch /etc/apache2/apache2.conf 
amey@amey-xps:~/$
```

Not only sudo, Bang (!) can do may more things :sunglasses:

### Repeat last command
!!

### Repeat last command that started with x
!x

### Repeat last command that has the substring x
!?x

### Repeat 10th command in the history file
!10

### Repeat 10th from last command in the history file
!-10
