# vscode setup

This is my vscode setup for developing Linux on a mac.  It uses qemu native on osx to execute the results, hopefully hyp mode will get debugging support soon as this will make things a lot quicker.

Documentation is pretty poor right now, I'll try a fresh install so I can find what I have already forgotten about this setup.

# pre-requisites

## Homebrew install of libvirt and qemu

- instructions for installing homebrew: https://brew.sh
- this setup based on information here:
   - https://libvirt.org/macos.html
   -  

```
% brew install qemu libvirt
% brew services restart libvirt
% echo 'security_driver = "none"' >> /opt/homebrew/etc/libvirt/qemu.conf
% echo "dynamic_ownership = 0" >> /opt/homebrew/etc/libvirt/qemu.conf
% echo "remember_owner = 0" >> /opt/homebrew/etc/libvirt/qemu.conf
```

Copy vscode directory to the root of your workspace as .vscode and modify to suite your setup

## Setup virtual machines

Once everything is connected make sure you install the VM description:
(this should probably be a task)

'''
% virsh -c qemu+tcp://gateway.docker.internal/session define .vscode/DebugKernel-arm64.xml
'''

## volume mount points

- I use an images directory in my home dir as /boot, so qemu can access results from make install, but its imperfect as what I really want is the Image file, not the vmlinuz file
- I use volume mounts for the linux workspace, the build directory, and the ccache directory to keep things quick


# TODO

- add a non-debug quick mode which using hypervisor mode to execute underlying kernel
- integrate u-root
- integrate perf for kernel tracing
