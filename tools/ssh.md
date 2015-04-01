SSH
===
**Create key**

```bash
ssh-keygen -t rsa -f ~/.ssh/id_rsa -P ''
```

**Copy public key to remote machine**

```bash
ssh-copy-id root@<REMOTE_HOST>
```

**Initiate port forwarding**

```bash
ssh -NL *:8086:<REMOTE_HOST>:8086 root@<REMOTE_HOST>
```

**Forward remote port to local**

```bash
ssh -NR *:1234:localhost:80 root@<REMOTE_HOST>
```
(`GatewayPorts yes` in `sshd_config` required to bind to non-loopback interface)
