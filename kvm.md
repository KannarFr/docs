# KVM

## Check if KVM module is available

`egrep --color=auto 'vmx|svm|0xc0f' /proc/cpuinfo
`

## List KVM modules

`zgrep CONFIG_KVM /proc/config.gz
`

## Create image

`qemu-img create archlinux.img 10G`

## Run VM from iso on image

`qemu-system-x86_64 -enable-kvm -boot d -cdrom archlinux-2017.12.01-x86_64.iso -m 512 -hda archlinux.img`

## OVMF (Open Virtual Machine Firmware)

First install `ovmf` packet.

Then create local copy of the non-volatile variable store for VM : `cp /usr/share/ovmf/ovmf_vars_x64.bin my_uefi_vars.bin`

Finally, add options to `qemu-system-x86_64` :

`-drive if=pflash,format=raw,readonly,file=/usr/share/ovmf/ovmf_code_x64.bin -drive if=pflash,format=raw,file=my_uefi_vars.bin`
4
## Networking

On host machine create bridge 

`ip link add BRIDGE-NAME type bridge`


Configure QEMU to handle bridges by writing `allow BRIDGE-NAME` in `/etc/qemu/bridge.conf`

