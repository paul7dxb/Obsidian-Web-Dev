```bash
SSH root@IP
```

Removing known host at IP (after rebuild)

```bash
 ssh-keygen -f "/home/mcpapa/.ssh/known_hosts" -R "139.162.193.12"
```

# Set up SSH key based Auth

```bash
mkdir -p ~/.ssh

```

On host machine
```bash
ssh-keygen -b 4096
```

Public key is id_rsa.pub
Copy to server
```bash
scp ~/.ssh/id_rsa.pub mcpapapps@139.162.193.12:~/.ssh/authorized_keys
```

On server
```bash
sudo chmod 700 ~/.ssh/ && sudo chmod 600 ~/.ssh/*
exit
```

# Prevent root login or password login

```bash
ssh mcpapapps@139.162.193.12

sudo nano /etc/ssh/sshd_config
```

```
PermitRootLogin no
PasswordAuthentication no
```

```bash
 sudo systemctl restart sshd
```