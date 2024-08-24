To show available NFS shares:

```shell session
 showmount -e VICTIMIP
```

Mounting and NFS Share:

```shell session
mkdir target-NFS
sudo mount -t nfs target_IP:/ ./target-NFS/ -o nolock
cd target-NFS
tree .
```

