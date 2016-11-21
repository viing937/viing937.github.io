# ArchLinux

It is a installation guide.

## 1. Preparation

### Connect to the Internet

#### wired

The ```dhcpcd``` daemon is enabled on boot for wired devices, and will attempt to start a connection. 

#### Wireless

```
$ wifi-menu
```

### Update the system clock

```
$ timedatectl set-ntp true
```

## 2. Prepare the storage devices

### Partition the devices

```
$ fdisk /dev/sdx
```

### Format the partitions

```
$ mkfs.ext4 /dev/sdxy
```

### Mount the partitions

```
$ mount /dev/sdxy /mnt
```

```
$ mkdir /mnt/home
$ mount /dev/sdxy /mnt/home
```

## 3. Installation

### Select the mirrors

```
$ vim /etc/pacman.d/mirrorlist
```

### Install the base packages

```
$ pacstrap -i /mnt base base-devel
```

## 4. Configuration

### fstab

```
$ genfstab -U /mnt >> /mnt/etc/fstab
```

### Change root

```
$ arch-chroot /mnt /bin/bash
```

### Locale

```
$ vim /etc/locale.gen
$ locale-gen
$ echo LANG=en_US.UTF-8 > /etc/locale.conf
```

### Time

#### Select a time zone

```
$ ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

#### Set the time standard to UTC

```
$ hwclock --systohc --utc
```

### Network configuration

#### Hostname

```
$ echo <hostname> > /etc/hostname
```

It is recommended to append the same host name to ```/etc/hosts```, for example:

```
$ cat /etc/hosts
127.0.0.1   localhost.localdomain   localhost    <hostname>
::1         localhost.localdomain   localhost    <hostname>
```

#### Wired

```
$ systemctl enable dhcpcd
```

#### Wireless

```
$ pacman -S iw wpa_supplicant dialog
$ wifi-menu
```

### Boot loader

```
$ pacman -S grub os-prober
$ grub-install --recheck /dev/sdx
$ grub-mkconfig -o /boot/grub/grub.cfg
```

### Root password

```
$ passwd
```

## 5. Unmount the partitions and reboot

```
$ umount -R /mnt
$ reboot
```

## 6. Post-installation

### Users and groups

```
$ useradd -m -g users -G wheel -s /bin/bash ving
$ passwd ving
```

```
$ vim /etc/sudoers
```

### Graphical user interface

```
$ pacman -S gnome
$ pacman -S gdm
$ systemctl enable gdm
```

### Networkmanager

```
$ pacman -S networkmanager
$ systemctl enable NetworkManager
```

### Proxy

#### Shadowsocks

```
$ pacman -S shadowsocks
$ vim /etc/shadowsocks/example.json
$ systemctl enable shadowsocks@example
```

#### Proxychains

```
$ pacman -S proxychains-ng
$ vim /etc/proxychains.conf
```

### AUR helper

```
$ git clone https://aur.archlinux.org/package-query.git
$ cd package-query
$ makepkg -si
```

```
$ git clone https://aur.archlinux.org/yaourt.git
$ cd yaourt
$ makepkg -si
```

### Input devices

#### Touchpad Synaptics

```
$ pacman -S xf86-input-synaptics
```

#### TrackPoints

```
$ pacman -S xf86-input-libinput
```

### Fonts

```
$ pacman -S ttf-dejavu wqy-microhei
```

### Chinese input method

```
$ pacman -S fcitx-im fcitx-configtool
```

```
$ vim ~/.xprofile
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```

Disable iBus.

```
$ gsettings set org.gnome.settings-daemon.plugins.keyboard active false
```

Reboot and configure fcitx.

```
$ fcitx-configtool
```

### Vim plugins

```
$ pacman -S vim-supertab
$ pacman -S vim-syntastic
$ pacman -S vim-nerdtree
$ pacman -S vim-taglist
```

### Other

#### Install some tools

```
$ pacman -S bash-completion
$ pacman -S pkgfile
$ pacman -S moreutils wireless_tools net-tools dosfstools
```

#### Load [configuration](/md/arch_config.md)
