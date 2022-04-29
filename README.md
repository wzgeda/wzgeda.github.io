```shell
## modify source 
vim /etc/pacman.d/mirrorlist
Server = https://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch
pacman -Sy
## partition
fdisk /dev/sda
mkfs.ext4 /dev/sda1
mount /dev/sda1 /mnt
## install package
pacstrap /mnt base linux linux-firmware dhcpcd xorg-server xorg-xinit xterm \
openbox xf86-video-nouveau wqy-microhei ttf-dejavu chromium sudo grub
## genfstab
genfstab -U /mnt >> /mnt/etc/fstab
## arch-chroot
arch-chroot /mnt
## locale
vim /etc/locale.gen
en_US.UTF-8 UTF-8
locale-gen
vim /etc/locale.conf
LANG=en_US.UTF-8
## dhcp
systemctl enable dhcpcd
## modify root passwd
passwd root
## add user
useradd -m free
passwd free
## sudo add new user
chmod 640 /etc/sudoers
vim /etc/sudoers
chmod 440 /etc/sudoers
## login new user
su - free
## openbox
mkdir -p ~/.config/openbox
cp -a /etc/xdg/openbox ~/.config
vim ~.xinitrc
exec openbox-session
## grub
grub-install --target=i386-pc /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
## reboot start xdg
reboot
startx

## configure archlinuxcn source 
## app
rox fcitx shadowsocks-qt5 pnmixer obconf google-chrome lxdm tint2 feh alsa-utils
## xterm conf
~/.Xresources
xterm*faceName:WenQuanYi Micro Hei Mono:pixelsize=16
xterm*faceNameDoublesize:WenQuanYi Micro Hei Mono:pixelsize=16
xrdb ~/.Xresources
## fcitx conf
vim /etc/profile.d/fcitx.sh
#!/bin/bash
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
## openbox autostart conf
vim ~/.config/openbox/autostart
tint2 &
feh --bg-scale xxx.jpg &
xrdb ~/.Xresource &
shadowsocks-qt5 &
pnmixer &
vim ~/.config/openbox/environment
LANG=zh_CN.UTF-8
```
