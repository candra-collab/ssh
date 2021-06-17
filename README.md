# ssh
1. Step by step configure SSH:
 - Sudo apt install openssh-server
 - Ssh username@ip -p 22122 
2. The /etc/ssh/sshd_config file contains configuration specifications for sshd. The
command below sets the owner and group of the file to root.
chown root:root /etc/ssh/sshd_config
chmod 600 /etc/ssh/sshd_config
3. Harning your ssh file : nano /etc/ssh/sshd_config

    a. To disable the OpenSSH V1 protocol and use the more secure OpenSSH V2
       protocol and port :
       
       - Protocol 2
       - port 22 change to be port 22022 (up to you)

    b. To disable unnecessary functions and avoid X11, TCP forwarding, and agent
        forwarding.
        
        - X11Forwarding no
        - AllowTcpForwarding no
        - AllowAgentForwarding no


     c. To prevent users from using environmental variables and to escape authentication
        using self-defined scripts:
        
        - PermitUserEnvironment no


     d. To avoid DNS query and reduce user login duration:
     
        - UseDNS no


     e. To forbid the TCP connection:
     
        - TCPKeepAlive no


     f. To forbid the root user from logging in directly and reduce the risk of leaking the
         password:
         
        - PermitRootLogin no


     G. To start using more secure encryption algorithms and hashing algorithms and
        reduce the risk of the system being attacked:
        
        - Ciphers aes256-ctr,aes192-ctr,aes128-ctr
        - MACs hmac-sha2-512,hmac-sha2-256


    h. To prohibit the remote host from connection the local forwarding port:
    
        - GatewayPorts no


    i. To prohibit the content of the motd file in the etc directory from being printed upon
        each interactive login.
        
        - PrintMotd no


    j. To set the banner information that displays alarms when a user connects the SSH:
    
        - Banner /etc/issue.net


    k. To set logging rules and record user login details:
    
        - LogLevel INFO
        - Subsystem sftp /usr/libexec/openssh/sftp-server -f AUTH -l INFO


    l. The IgnoreRhosts parameter specifies that .rhosts and .shosts files will not be used
       in RhostsRSAAuthentication or HostbasedAuthentication:
       
        - IgnoreRhosts yes


    m. Even though the .rhosts files are ineffective if support is disabled in /etc/pam.conf,
        disabling the ability to use .rhosts files in SSH provides an additional layer of protection:
        
        - HostbasedAuthentication no


    n. Disallowing remote shell access to accounts that have an empty password reduces the probability of unauthorized access to the system:
    
        - PermitEmptyPasswords no


    o. To set the SSH idle timeout time:
    
        - ClientAliveInterval 300
        - ClientAliveCountMax 0


    p. To set the maximum number of failed authentication attempts and prevent bruteforce cracking:
    
        - MaxAuthTries 2


    q. To disable Kerberos authentication :
    
        - KerberosOrLocalPasswd no


**NOTE : if you want secure, you can config use it according to what you need !!!**

4. Restart the SSH :
    - systemctl restart sshd
5. create ssh key user : 
    - ssh-keygen -t rsa
  ssh keygen using username :
    - ssh -keygen -t rsa -b 4096 -C 'username'

4. how to used ssh keygen, after that you can register the server key from the user :
  - cd ~/.ssh
  - ls
  - cat id_rsa.pub 
  - cp id_rsa.pub >> authorized_keys

5. chown and chmod (file permission) 
    chmod 700 ~/.ssh
    Chmod 600 ~/.ssh/authorized_keys
    **
** **NOTE : if your password correct but cant connect ssh, because file permission. you can rolback to be default file permission**.
**
