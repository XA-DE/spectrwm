#BASE ISO

#STEPS FOR INSTALLATION
#for PC
su
ip link est wlan0 up
rfkill unblock wifi #if above commands results as error
ip link set wlan0 up
connmanctl
scan wifi
services
agent on
connect <wifi-id>
#passwd
quit

#for VM
lsblk
cfdisk /dev/sda
mkfs.fat -F32 /dev/sda1
mkfs.ext4 /dev/sda2
mount /dev/sda2 /mnt
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
basestrap /mnt base elogind-runit git xf86-video-<>
fstabgen -U /mnt >> /mnt/etc/fstab
artools-chroot /mnt
git clone https://github.com/XA-DE/<>.git
exit
umount -R /mnt
reboot
ln -s /etc/runit/sv/NetworkManager /run/runit/service/NetworkManager
#configure /etc/xdg/picom
