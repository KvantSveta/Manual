# Hdd

```bash
sudo blkid
```

> /dev/mmcblk0p1: LABEL="boot" UUID="0763-6493" TYPE="vfat" PARTUUID="f977252e-01"
>
> /dev/mmcblk0p2: UUID="734d7a6d-e6b2-4d91-8978-192f695c8e5e" TYPE="ext4" PARTUUID="f977252e-02"
>
>/dev/sda1: LABEL="Cronos" UUID="7e0e1084-33bf-44f8-8796-d67ed6200bad" TYPE="ext4" PARTUUID="000f07cf-01"
>
> /dev/mmcblk0: PTUUID="f977252e" PTTYPE="dos"

```bash
sudo blkid -o full -s UUID
```

> /dev/mmcblk0p1: UUID="0763-6493"
>
> /dev/mmcblk0p2: UUID="734d7a6d-e6b2-4d91-8978-192f695c8e5e"
>
> /dev/sda1: UUID="7e0e1084-33bf-44f8-8796-d67ed6200bad"

**опции, указываемые при монтировании тома**

> defaults = exec,auto,rw,nouser,async,nosuid,atime
>
> defaults,noauto,user = exec,noauto,rw,user,async,nosuid,atime

```bash
cat /etc/fstab
```
> proc            /proc           proc    defaults          0       0
>
> PARTUUID=f977252e-01  /boot           vfat    defaults          0       2
>
> PARTUUID=f977252e-02  /               ext4    defaults,noatime  0       1
>
> UUID=7e0e1084-33bf-44f8-8796-d67ed6200bad /media ext4 defaults,noauto,user 0 2

**монтирование hdd**

```bash
mount /media
```