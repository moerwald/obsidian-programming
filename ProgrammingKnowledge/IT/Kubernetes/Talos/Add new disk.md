
Einfach ein `disk_patch.yaml` anlegen:

```yaml

machine:
    disks:
        - device: /dev/sdb # The name of the disk to use.
          # A list of partitions to create on the disk.
          partitions:
            - mountpoint: /mnt/storage_persistent # Where to mount the partition.
	
```


Das Patchfile kann via :

```
talosctl patch machineconfig --patch-file .\disk_patch.yaml -n 10.146.3.136
```

applied werden.

#Talos
#Disk