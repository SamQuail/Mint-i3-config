# Mint-i3-config

## Install 
```bash
sudo apt install  i3-wm i3lock i3status polybar feh rofi scrot python3 python3-pip
```
```bash
sudo snap install alacritty --classic
```
### Arch extra installs
On arch there is no default login already installed by the OS, so you need to install something like lightdm

```bash
sudo apt install lightdm lightdm-gtk-greeter
```
To enable the lightdm service

```bash
sudo systemctl enable lightdm.service
```
Tp Run lightdm

```bash
sudo systemctl start lightdm.service
```
