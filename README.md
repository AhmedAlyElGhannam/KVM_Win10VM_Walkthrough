# KVM_Win10VM_Walkthrough

I got sick of Windows but I still need it to use programs like Matlab, Altium, and Solidworks. So, I decided to install them on a windows VM instead of dual booting on my Thinkpad P53. Ergo, this is a guide on how to install a Windows 10 VM on KVM cuz Virtualbox is for noobs. 

## Prerequisites
```bash
sudo apt install -y qemu qemu-kvm libvirt-daemon libvirt-clients bridge-utils virt-manager
sudo apt install -y qemu qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager virtinst cpu-checker
sudo apt install -y qemu-system qemu-user qemu-user-static
sudo apt install -y qemu-system-arm qemu-system-mips qemu-system-ppc qemu-system-sparc qemu-system-x86
sudo systemctl enable libvirtd
sudo systemctl start libvirtd
sudo systemctl status libvirtd
sudo usermod -aG kvm $USER
sudo usermod -aG libvirt $USER
```

## Creating a Virtual Hard Disk (200GB in my case)
```bash
qemu-img create -f qcow2 /home/nemesis/Storage/Win10VM/win10disk.qcow 200G
```

## Installing Windows 10 on Virtual Hard Disk (For The First Time Using ISO)
```bash
sudo virt-install   --name win10   --ram 16384   --vcpus 8   --os-variant win10   --disk path=/home/nemesis/Storage/Win10VM/win10_disk.qcow2,format=qcow2,size=200   --cdrom /home/nemesis/Downloads/en-us_windows_10_consumer_editions_version_21h2_x64_dvd_6cfdb144.iso   --network network=default   --graphics spice
```

### Importing an existing VM

```bash
virt-install \
--name windows10 \
--ram 16384 \
--vcpus 8 \
--os-type windows \
--os-variant win10 \
--disk path=/var/lib/libvirt/images/windows10.qcow2,format=qcow2 \
--network network=default \
--graphics spice \
--import
```
