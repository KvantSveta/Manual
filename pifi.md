# PiFi DAC+ V2.0

**set pifi as default card**
```bash
sudo touch /etc/asound.conf

pcm.!default  {
    type hw
    card 1
}

ctl.!default {
    type hw 
    card 1
}

```

**change boot config for run pifi dac**
```bash
/boot/config.txt
dtparam=i2s=on
dtoverlay=hifiberry-dacplus
```