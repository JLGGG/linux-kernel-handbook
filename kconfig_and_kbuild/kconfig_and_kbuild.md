# Kconfig & Kbuild

Kernel configuration is start point to make our kernel. This configuration focus on making kernel v6.15.0 based on an x86 system. The Kconfig* files contain metadata interpreted by the kernel's config and build system.   
Kconfig file at the root of the kernel source tree is used to make the initial menuconfig's UI. Kconfig is consisted of hierarchy, which different folders have the other Kconfig. 
```
make mrproper # It cleans everything, including the .config if it exists. 
```
Tuned kernel config as the localmodconfig
```
lsmod > /tmp/lsmod.now
cd ${KSRC}
make LSMOD=/tmp/lsmod.now localmodconfig

make menuconfig # configuration using GUI   
# Change the value by pressing the spacebar.
# [*]: On, feature compiled and built in the kernel image
# [ ]: Off, not built at all
# <*>: On, feature compiled and built in the kernel image
# <M>: Module, feature compiled and built as a kernel module
# < >: Off, not built at all
```

Building the kernel is indeed a very memory- and CPU-intensive job. I recommend you to switch from GUI to CLI. We must also finish kernel configuration before starting make.
```
sudo systemctl isolate multi-user.target # No GUI
sudo systemctl isolate graphical.target # come back to GUI

make -j$(nproc) # root of kernel source tree
```
After finishing build, bzImage is located in "arch/< arch >/boot/."

Install kernel module to /lib/modules
```
sudo make modules_install
```

Generate initramfs (initial RAM filesystem) in /boot
```
sudo make install
```