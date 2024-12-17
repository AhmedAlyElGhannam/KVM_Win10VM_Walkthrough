# KVM_Win10VM_Walkthrough



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
