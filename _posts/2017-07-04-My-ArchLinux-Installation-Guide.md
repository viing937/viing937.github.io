---
title: My ArchLinux Installation Guide
layout: post
---

* TOC
{:toc}

It is a ArchLinux installation guide.

# 1. Preparation

## 1.1 Connect to the Internet

If your device is wired, the `dhcpcd` daemon is enabled and will attempt to start a connection, otherwise

```
$ wifi-menu
```

## 1.2 Update the system clock

```
$ timedatectl set-ntp true
```

# 2. Prepare the storage devices

## 2.1 Partition the devices

```
$ fdisk /dev/sdx
```

## 2.2 Format the partitions

```
$ mkfs.ext4 /dev/sdxy
```

## 2.3 Mount the partitions

```
$ mount /dev/sdxy /mnt
```

```
$ mkdir /mnt/home
$ mount /dev/sdxy /mnt/home
```

# 3. Installation

## 3.1 Select the mirrors

```
$ vim /etc/pacman.d/mirrorlist
```

## 3.2 Install the base packages

```
$ pacstrap -i /mnt base base-devel
```

# 4. Configuration

## 4.1 fstab

```
$ genfstab -U /mnt >> /mnt/etc/fstab
```

## 4.2 Change root

```
$ arch-chroot /mnt /bin/bash
```

## 4.3 Locale

Uncomment `en_US.UTF-8 UTF-8` and `zh_CN.UTF-8 UTF-8`.
```
$ vim /etc/locale.gen
```

```
$ locale-gen
$ echo LANG=en_US.UTF-8 > /etc/locale.conf
```

## 4.4 Time

```
$ ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
$ hwclock --systohc --utc
```

## 4.5 Network configuration

```
$ echo <hostname> > /etc/hostname
```

## 4.6 Boot loader

```
$ pacman -S grub os-prober
$ grub-install --recheck /dev/sdx
$ grub-mkconfig -o /boot/grub/grub.cfg
```

## 4.7 Root password

```
$ passwd
```

# 5. Unmount the partitions and reboot

```
$ umount -R /mnt
$ reboot
```

# 6. Post-installation

## 6.1 Add user

```
$ useradd -m -g users -G wheel -s /bin/bash ving
$ passwd ving
```

Allow users in `wheel` group use `sudo` command.

```
$ vim /etc/sudoers
```

## 6.2 Graphical user interface

```
$ pacman -S gnome
$ systemctl enable gdm
```

## 6.3 Networkmanager

```
$ systemctl enable NetworkManager
```

## 6.4 Proxy

Shadowsocks.

```
$ pacman -S shadowsocks
$ vim /etc/shadowsocks/example.json
$ systemctl enable shadowsocks@example
```

Proxychains.

```
$ pacman -S proxychains-ng
$ vim /etc/proxychains.conf
```

## 6.7 Input devices

if you are using a laptop

```
$ pacman -S xf86-input-synaptics
```

if your your laptop has a TrackPoint

```
$ pacman -S xf86-input-libinput
```

## 6.8 Fonts

```
$ pacman -S wqy-microhei
```

## 6.9 Chinese input method

```
$ pacman -S fcitx-im fcitx-configtool
```

The `xprofile` is contained in my dot files.

```
$ vim ~/.xprofile
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```

Reboot and configure fcitx.

```
$ fcitx-configtool
```

## 6.10 Other

Fetch my dot files.

```
$ git clone https://github.com/viing937/dotfiles.git ~/.dotfiles
$ ~/.dotfiles/install.sh
```
