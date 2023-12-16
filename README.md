# My Linux

This is a repository I will handle some files or annotations about my Linux personal use.

To install WSL:
- `wsl --install` | `wsl --install -d Ubuntu`

Show all Linux distro installed:
- `wsl -l -v`

To remove Ubuntu:
- `wsl --unregister Ubuntu`

Download Arch Linux file:
- Go to this[https://github.com/yuk7/ArchWSL] repository and search for the zip file in *Docs > How to setup > 'Download' link on 'Method 1: zip file'*. Now extract the files and run `Arch.exe`.
- After close the console, open `Arch.exe` again and wait it make the final configurations. When console show *[root@PC-NAME]#*, type *passwd* and define your root password. Now type:
    - `echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel`, to setup sudoers file.
    - `useradd -m -G wheel -s /bin/bash {username}`, where '{username}' is your root username (without brackets).
    - `passwd {username}`, to set default user password (you can repeat last password if you want).
    - `exit`
- Open Windows Terminal on the folder you extracted Arch.zip and then run `.\Arch.exe config --default-user {username}`.
- Run *Arch.exe* again and congratulations, you already have an Arch Linux running in your machine.

Update your Pacman:
- `sudo pacman-key --init`
- `sudo pacman-key --populate`
- `sudo pacman -Syy archlinux-keyring`
- `sudo pacman -Syyuu`

Install wget:
- `sudo pacman -Sy wget openssh`

Install Yay (needed to use AUR):
- `sudo pacman -S --needed git base-devel`
    - Install fakeroot? **NO**
    - Enter a selection: just press *Enter* and you'll select all.
    - Proceed with installation? **YESS**
- `cd /tmp`
- `git clone https://aur.archlinux.org/yay.git`
- `cd yay`
- `makepkg -si`

Windows Terminal:
- Install by Windows Store

ZSH:
- `yay -Sy zsh`
