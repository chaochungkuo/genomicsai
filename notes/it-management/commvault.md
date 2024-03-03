# Commvault

### Uninstall in Ubuntu

1. On client run `commvault stop` (this may not work if broken)
2. Run `ps -ef`` `_`|`_` ``grep -i commvault` command to make sure no CV processes are running. If there is a process running, run `kill -9 <pid>` to kill it.
3. Run `rm -rf /etc/CommVaultRegistry`
4. Run `rm -rf /opt/commvault`        &#x20;
5. Run `rm -rf /tmp/.gxset*`          &#x20;
6. Run `rm -rf /var/log/commvault/*`  &#x20;

<pre><code><strong>sudo rm -rf /etc/CommVaultRegistry
</strong>sudo rm -rf /opt/commvault
sudo rm -rf /tmp/.gxset*
sudo rm -rf /var/log/commvault
</code></pre>

### Reference

* [How to cleanup/uninstall MediaAgent application on Linux?](https://community.commvault.com/commvault-q-a-2/how-to-cleanup-uninstall-mediaagent-application-on-linux-484)
