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
openbox xf86-video-nouveau wqy-microhei ttf-dejavu chromium sudo
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
## reboot start xdg
reboot
startx
```
