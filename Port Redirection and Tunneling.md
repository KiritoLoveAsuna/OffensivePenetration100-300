### Port Forwarding
###### RINETD
```
cat /etc/rinetd.conf
...
# bindadress    bindport  connectaddress  connectport
0.0.0.0 80 142.0.128.189  22
...
service rinetd start
```
###### SSH local port forwarding
bind port 445 on our local machine (0.0.0.0:445) from ssh protocol to port 445 on the Windows Server (192.168.1.110:445) and do this through a session to our original Linux target, logging in as student (student@10.11.0.128)
```
sudo ssh -N -L 0.0.0.0:445:192.168.1.110:445 student@10.11.0.128
```
###### ssh remote port forwarding
```
ssh -N -R 10.11.0.4:2221:127.0.0.1:3306 kali@10.11.0.4
```
>This will forward all incoming traffic on our Kali system's local port 2221 to port 3306 on the compromised box through an SSH tunnel (TCP 22), allowing us to reach the MySQL port even though it is filtered at the firewall.
![image](https://user-images.githubusercontent.com/38044499/223974570-2d8384c0-b01d-46d2-b200-45dd3906ee92.png)