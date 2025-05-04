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

## Picom

When it comes to Picom forget everything what the docs and YouTube says concerning the features Picom has, its all outdated. Base Picom does have `dual_kawase` blur, curved corners and shadows, so I wouldn't bother with the hassle of using the next branch or using a fork.

## Virtualization

if you want to run Windows apps on Linux but dont want to go through the pain of trying to get Wine to work, KVM with QEMU and libvirt is a good compromise.

### Virtualisation comparability  

Run `lscpu | grep -i virtualization` to check if your installation supports virtualization, the output should be `VT-x` or `AMD-V`, if nothing it outputted you need to enable virtualisation if your BIOS.

Next run `zgrep CONFIG_KVM /boot/config-$(uname -r)` to check if your installation has KVM modules installed, it is installed if it is set to `y` or `m`.

## Installing virtualization packages

As KVM is already installed on Linux, we only need to install libvirt and qemu-kvm, wit

```bash
sudo apt install qemu-system-x86 libvirt-daemon-system virtinst virt-manager virt-viewer ovmf swtpm qemu-utils guestfs-tools libosinfo-bin tuned
```

for windows VMs you also need to install `virtio` drivers for KVM. [download link](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/virtio-win-0.1.271-1/)

with libvirtd you have two options: monolthic vs modular daemons. The main difference is the old version is a single central daemon, which exposes all stateful drivers. Basically using the modular libvirtd means each driver has its own daemon, giving you the ability to pick and choose what drivers you want to use, which will definitely increase performance and reduce resource usage compared to the monolithic way

## validating KVM

to validate the install run `sudo virt-host-validate qemu`. If you have an Intel CPU you can fairly confidently disregard the `QEMU: Checking for secure guest support` warning, if your on AMD google it, there a command you need to run. If you get `QEMU: Checking if IOMMU is enabled by kernal` as a warning, you need to goto into the grub file, by `sudo vim /etc/default/grub` and then edit `GRUB_CMDLINE_LINUX=` to also have `intel_iommu=on iommu=pt`. Then regenerate the grub file, `sudo grub2-mkconfig -o /boot/grub2/grub.cfg`, then do a reboot.   

## Using KVM

if when opening virt manager it says KVM is unavailable, enter `sudo virt-manager` in the console rather then just clicking on the gui shortcut

## Anti-virus