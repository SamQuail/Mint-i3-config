# Mint-i3-config

## Install 
```bash
sudo apt install  i3-wm i3lock i3status polybar feh rofi scrot python3 python3-pip vim picom sxhkd
```
```bash
sudo snap install alacritty --classic
```
### Arch extra installs
On arch there is no default login already installed by the OS, so you need to install something like lightdm

```bash
sudo pacman -S lightdm lightdm-gtk-greeter
```
To enable the lightdm service

```bash
sudo systemctl enable lightdm.service
```
Tp Run lightdm

```bash
sudo systemctl start lightdm.service
```
 
 ## Oh My Zsh install
 ```bash
 sudo apt install zsh
 ```
Installing nerd fonts

```bash
mkdir -p ~/.local/share/fonts
cd ~/.local/share/fonts && curl -fLO https://github.com/ryanoasis/nerd-fonts/raw/HEAD/patched-fonts/DroidSansMono/DroidSansMNerdFont-Regular.otf
```

in `./config/alacritty/alacritty.yml` add the following, though if you copy the config file it will already be there:
```bash
shell:
  program: /usr/bin/zsh
  args:
    - --login
```

To set zsh the default shell across all termainls run the following:
```bash
chsh -s $(which zsh)
```

actually install oh my zsh:
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
