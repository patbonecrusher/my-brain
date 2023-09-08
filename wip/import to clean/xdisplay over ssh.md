## setup
### on the server
```
# sudo vi /etc/ssh/sshd_config
AllowAgentForwarding yes
#AllowTcpForwarding yes
#GatewayPorts no
X11Forwarding yes
X11DisplayOffset 10
X11UseLocalhost yes
#PermitTTY yes
PrintMotd no
#PrintLastLog

```

### on client side

```
Host *
	ForwardAgent yes
	ForwardX11 yes
	ForwardX11Trusted yes
	Port 22
	Protocol 2
	ServerAliveInterval 60
	ServerAliveCountMax 30
```




### to test
```
# On client
export DISPLAY=:0

ssh nuc

# On server
echo $DISPLAY # make sure it is not empty if it is empty you client config is wrong
gnome-control-center # it should open on your computer
```


#### libGL error when using SSH and X forwarding with MacOS

[Weijun Gao](https://psycomp.utsc.utoronto.ca/support/index.php/author/gaoweiju/ "View all posts by Weijun Gao")Posted on [October 14, 2021](https://psycomp.utsc.utoronto.ca/support/index.php/2021/10/14/libgl-error-when-using-ssh-x-forwarding-with-macos/ "libGL error when using SSH and X forwarding with MacOS") Posted in [Cluster Info](https://psycomp.utsc.utoronto.ca/support/index.php/category/clusterinfo/), [Linux Shell](https://psycomp.utsc.utoronto.ca/support/index.php/category/linuxshell/)

If you use MacOS and “ssh -X” or “ssh -Y” to access the cluster, and you see the following error messages when start a GUI application on the cluster:

```
libGL error: No matching fbConfigs or visuals found
libGL error: failed to load driver: swrast
```

Running the following command after starting a Slurm session may fix the problem:

```
export LIBGL_ALWAYS_INDIRECT=1
```