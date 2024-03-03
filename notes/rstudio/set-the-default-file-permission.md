# Set the default file permission

Edit the file `/etc/rstudio/rserver.conf` (in Ubuntu) and add

```
server-set-umask=0
```

#### Reference

* [Rstudio Server Documentation, Access and Security, umask](https://docs.posit.co/ide/server-pro/1.2.1502-1/access-and-security.html)
* [What Is Umask and How to Use it Effectively](https://www.liquidweb.com/kb/what-is-umask-and-how-to-use-it-effectively/)
