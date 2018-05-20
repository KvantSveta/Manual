# SublimeText

download

```bash
wget https://download.sublimetext.com/sublime_text_3_build_3170_x64.tar.bz2
```

unpack it

```bash
tar -jxvf sublime_text_3_build_3170_x64.tar.bz2
```

move folder

```back
mv sublime_text_3 sublime_text
sudo mv sublime_text /opt
```

copy sublime_text.desktop

```bash
sudo cp /opt/sublime_text/sublime_text.desktop /usr/share/applications
```

change icon path in /usr/share/applications/sublime_text.desktop

```bash
Icon=/opt/sublime_text/Icon/32x32/sublime-text.png
```

create simlink to use sublime via subl

```bash
sudo ln -s /opt/sublime_text/sublime_text /usr/bin/subl
```
