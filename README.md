# My Linux

This is a repository I will handle some files or annotations about my Linux personal use.

To install WSL:
- `wsl --install` | `wsl --install -d Ubuntu`

Show all Linux distro installed:
- `wsl -l -v`

To remove Ubuntu:
- `wsl --unregister Ubuntu`

Download Arch Linux file:
- Go to [this repository](https://github.com/yuk7/ArchWSL) and search for the zip file in *Docs > How to setup > 'Download' link on 'Method 1: zip file'*. Now extract the files and run `Arch.exe`.
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

Power10k Theme:
- Go to [this repository](https://github.com/romkatv/powerlevel10k) and search for the zip file in *Installation > Arch Linux*. Run these commands:
    - `yay -S --noconfirm zsh-theme-powerlevel10k-git`
    - `echo 'source /usr/share/zsh-theme-powerlevel10k/powerlevel10k.zsh-theme' >> ~/.zshrc`

Define ZSH as default shell:
- `chsh -s /usr/bin/zsh`
- Close Arch WSL.

Installing additional fonts:
- In the same Power10k repository, go to *Fonts* and go to *Manual font installation* on the page. Download all the *.tff* files and install it on Windows as you install a *.exe* file.
- Right-click on Windows Terminal's top and go to *Settings > Arch > Appearance > Font face* and change it to **MesloLGS NF**.
- Close Windows Terminal and open it again with Arch.

Configuring Power10k:
- After open Arch right after configure ZSH, it will ask you to configure Power10k. **DO NOT** go ahead if you can't see correctly the symbols (like diamond, arrow etc.).

ZSH Auto Suggestion:
- Go to [this repository](https://github.com/zsh-users/zsh-autosuggestions) and go to *INSTALL.md > Manual*. Run these commands:
    - `git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions`
    - `echo 'source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh' >> ~/.zshrc`
- Note: If you only type `source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh` it will run just once, then you must type with `echo 'source...` to put it into *zshrc* file (like we did before with Power10k Theme), and then it'll run everytime you start your session.

Substitute commands (bat/cat, fd/find etc.):
- `yay -Sy bat exa fd ripgrep procs grex`
This command will install all of these listed new commands, that substitutes:

    | old | new |
    | --- | --- |
    | cat | bat |
    | exa | ls |
    | find | fd |
    | grep | ripgrep |
    | ps | procs |
    | x | grex |

To made alias for these commands:
- `alias cat=bat`, for example, to everytime you write `cat` the terminal will understand as `bat`, and then you can use the new commands just by using the old commands. But the bad new about it is that you must type this alias everytime you open again your terminal. So, to make it permanently, you can create a *.alias* file and type all the aliases you want.
- `vim ~/.alias`
*ooooooooooor...*
You can download my personal *.alias* file that I put in this repository, by typing this command:
- `wget -c https://dioscar90.github.io/mylinux/alias.txt -O ~/.alias`
After, type it to put all of these alises automatically in *.zshrc* evertytime you open your terminal:
- `echo 'source ~/.alias' >> ~/.zshrc`

ASDF, to run multiples versions of languages:
- `yay -Sy asdf-vm`
You can set *yes* for all default options.
Now you must turn it initialized everytime you open your terminal, as you do with your *.alias* file:
- `echo 'source /opt/asdf-vm/asdf.sh' >> ~/.zshrc`
Now we'll install a list of common languages. You can install if you want, and install others you want as well (go to [this repository](https://github.com/asdf-vm/asdf-plugins) and surch for the plugin you want). This three commands will 1) Install plugin of *nodejs*; 2) List all *nodejs* versions; 3) Install *nodejs* on the version you want; 4) Set the version you want to be the global (or default) version of your machine:
- `asdf plugin add nodejs https://github.com/asdf-vm/asdf-nodejs.git`
- `asdf list-all nodejs`
- `asdf install nodejs 21.4.0` or `asdf install nodejs latest`
- `asdf global nodejs 21.4.0` or `asdf global nodejs latest`
Now, if you run `node -v` you will get `21.4.0` in your console.
If there is a project you need to run a different version of node, you can go to the root of that project and then type:
- `asdf local nodejs <version-you-want>`
That way, only that repository will run that version of *nodejs*. Of course, be sure you already have that parcitular version already installed in you machine. If not, install it, by typing `asdf install nodejs <version-you-want>` (as we did above).
Repeat it for all languages you want. In my case:
- .NET
- nodejs
- Python
- PHP (after install the plugin, install):
    - `yay -Sy re2c gd postgresql-libs libzip`
    Then, *list-all*, *install* (tooooo long time...) and set as *global*. After:
    <!-- - `php -m | grep mysql`, and you'll see that MySQL is installed. -->
    <!-- - `php -m | grep imagick`, and you'll see that ImageMagick is **not** installed. -->
    - `yay -Sy imagemagick`
    - `pecl install imagick`
    - *Please provide the prefix of ImageMatick installation [autodetect]* -> Press Enter.
    <!-- - `echo "extension=imagick.so" >> $(asdf where php)/conf.d/php.ini` -->
    <!-- - `php -m | grep imagick`, and you'll see that ImageMagick **is** installed. -->
    - `pecl install redis`
    - `echo "extension=redis.so" >> $(asdf where php)/conf.d/php.ini`

Docker:
- Download it by the [Docker official website](https://www.docker.com/) (pay attention to download the **Windows's** option).
- After install and restart your PC, open Docker.
- Navegate to *Settings (⚙️) > Resources > WSL integration* and allow **Arch**.
- Click **Apply**.
- Close Docker and also exit Arch WSL. Then, restart both.
- Type `docker` in Arch. If it say that Docker is not installed yet and ask you to install, **do not** do it. Try to close all and restart again. If necessary, restart your PC.
- Once `docker` run, type `docker ps` and you'll see that there is non container yet.
- Now you can add some images, for example:
    - `docker run -d -p 80:80 docker/getting-started`
- After configure this container, type `docker ps` again and you'll see it running.
- Go to `localhost` and you can see the Docker's Getting Started Page.
- Now you can stop this container (on Windows) and also remove, because it's useless.
