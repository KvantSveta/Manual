# mdadm

Первый диск определяется ОС как /dev/sda1, а второй диск как /dev/sdb1

#### Первоначальная подготовка дисков
```bash
sudo fdisk /dev/sda
Создание новой таблицы разделов:
g
Удаление всех разделов, если они есть:
d
Создание нового раздела:
n
Вывод получившейся таблицы разделов:
p
Запись всех изменений:
w
```

Предыдущий блок необходимо повторить для второго диска

#### On RPi RAID 1
```bash
RAID-массив нельзя создавать поверх разделов, на которых находятся смонтированные ФС
sudo umount /dev/sda1
sudo umount /dev/sdb1

Создания RAID-массива
sudo mdadm --create /dev/md0 --verbose --level=1  --raid-devices=2 /dev/sda1 /dev/sdb1
OR
sudo mdadm -Cv /dev/md0 -l1  -n2 /dev/sda1 /dev/sdb1

Проверка состояния RAID-массива
cat /proc/mdstat
Просмотр состояния RAID-массива в real-time
watch cat /proc/mdstat

Подробная информация о RAID-массиве
sudo mdadm --detail /dev/md0

Ожидание синхронизации RAID-массива
```

#### Необходимо создать раздел на новом блочном устройстве
```bash
sudo fdisk /dev/md0
Создание новой таблицы разделов:
g
Создание нового раздела:
n
Вывод получившейся таблицы разделов:
p
Запись всех изменений:
w
```

#### Создание ФС
```bash
sudo mkfs.ext4 /dev/md0p1
```

#### Ручное монтирование RAID-массива
```bash
sudo mount /dev/md0p1 /media
```

#### Настройка файла mdadm.conf
```bash
sudo bash -c 'echo "DEVICE partitions" >> /etc/mdadm/mdadm.conf'
sudo bash -c 'mdadm --detail --scan --verbose | awk "/ARRAY/ {print}" >> /etc/mdadm/mdadm.conf'
```

#### Автоматическое монтирование RAID-массива при загрузке ФС
```bash
Запись в /etc/fstab
/dev/md0p1      /media     ext4    defaults    0 2
OR
UUID=d091bbb9-0a3c-4cea-9192-a8282ef8c36e  /media     ext4    defaults,noauto,user    0 2
```

#### Проверка целосности RAID-массива
```bash
sudo bash -c 'echo "check" > /sys/block/md0/md/sync_action'

Результат проверки
sudo cat /sys/block/md0/md/mismatch_cnt
```

#### Сборка RAID-массива после перезагрузки, если не прописан в /etc/fstab
```bash
sudo mdadm --assemble /dev/md0 /dev/sda1 /dev/sdb1
OR
sudo mdadm --assemble --scan
```

#### Остановка и удаление RAID-массива
```bash
sudo umount /dev/md0p1
sudo mdadm --stop /dev/md0
sudo mdadm --remove /dev/md0

Удаление суперблоков
sudo mdadm --zero-superblock /dev/sda1 /dev/sdb1

Полная очистка диска
sudo dd if=/dev/zero of=/dev/sda1 bs=1M status=progress conv=noerror
sudo dd if=/dev/zero of=/dev/sdb1 bs=1M status=progress conv=noerror

Очистка MBR
sudo dd if=/dev/zero of=/dev/sda1 bs=512 count=1
sudo dd if=/dev/zero of=/dev/sdb1 bs=512 count=1
```

#### Отображение UUID диска
```bash
sudo blkid -o full -s UUID
```