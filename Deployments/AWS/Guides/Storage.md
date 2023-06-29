# EBS Attached to linux

- [Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-using-volumes.html)

```bash
# List information about attached devices
sudo lsblk -f
```

- If volume isn't empty create a file system on the volume

```bash
sudo mkfs -t xfs /dev/xvdf
```

- Mount the volume to a folder (e.g /data)
```
sudo mkdir /data && sudo mount /dev/xvdf /data
```