## Getting internet to work ##

Make sure you installed networkmanager when installing the essential software

$ systemctl enable NetworkManager.service

$ systemctl start NetworkManager.service


## Creating regular user and giving him sudo perms ##

$ useradd -m -g wheel username

execute "visudo" and uncomment the wheel can execute root commends, should look like this: [%wheel ALL=(ALL) ALL]
write changes using :w and quit using :q

set up new user password by: "passwd username"

log into new user by: "su - username"

validate new user root permissions by: "sudo pwd"

you can go back to root user by "exit" 

## Installing Xorg server ##

$ pacman -S xorg-server xorg-xinit 


## Installing i3 window manager ##
$ pacman -S i3-gaps i3status i3blocks dmenu

Edit (or create) the .xinitrc in home directory of normal user and add "exec i3"

$ reboot

make sure to log in as non root user

type "startx" to start i3, you can make i3  autostart by adding "startx" to end of your .bash_profile file in home directory 

## i3blocks config ##

https://github.com/miklhh/i3blocks-config


## Installing Firefox browser ##

$ pacman -S firefox 

## Installing file Thunar file manager and essential plugins ##

$ pacman -S thunar 
$ pacman -S polkit-gnome gvfs thunar-volman ntfs-3g p7zip thunar-archive-plugin tumbler 


## Setting up AUR repos by installing YAY ##
$ git clone https://aur.archlinux.org/yay.git
$ cd yay/
$ makepkg -si
$ yay


#Installing fonts ##

$ nerd-fonts-complete (aur)
$ noto-fonts
$ noto-fonts-emoji 


## Setting up audio ##

$ pacman -S alsa pulseaudio pavucontrol

$pulseaudio --start

After that you can use "pavucontrol" for friendly way to manage audio 


## Other useful but not mandatory software (installed by "pacman -S name") ##

gnome-keyring (for applications using autologins to store creds)

curl (for curling lol)

rsync (best syncing program)

python2 (python)

python3 (python)

veracrypt (encryption and decryption suite)

dunst (allows notifications to pop up)

xfce4-settings (allows to select preferred application like for example "start terminal here" in thunar 

## Enable multilib repo (for steam and other nice software) ##
edit "/etc/pacman.conf":

Uncomment the following:
``
[multilib]
include = /etc/pacman.d/mirrorlis
``


## Create swapfile (optional) ##

$ sudo fallocate -l 8G /swapfile

$ sudo chmod 600 /swapfile

$ sudo mkswap /swapfile
$ echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

## Recuce swappiness (how aggresively system will use swap over actual ram, 60 is default, the lower the more of a last resort swap will be) ##

Create "/etc/sysctl.d/99-swappiness.conf" and add:
vm.swappiness=10 

## NTP (time) settings ##

$ set timezone: timedatectl set-timezone Europe/Warsaw
$ systemctl enable systemd-timesyncd
$ systemctl start systemd-timesyncd
