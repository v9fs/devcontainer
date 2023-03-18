# vscode setup

This is my vscode setup for developing Linux on a mac.

Documentation is pretty poor right now, I'll try a fresh install so I can find what I have already forgotten about this setup.
This repo uses the v9fs/docker container as a base image and the v9fs/vscode image for vscode task setup.

# pre-requisites (for native qemu)

If you want to run qemu native on the mac to take advantage of speed boosts from hypervisor mode,
you have to do this:

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

## Under the hood

The devcontainer scripts will take care of configuring vscode tasks and setting up libvirt virtual machine
definitions.  If you haven't taken care of the pre-requisits, the native qemu targets won't work and you'll just need
to run the qemu inside the docker.

# TODO

- [ ] add a non-debug quick mode which using hypervisor mode to execute underlying kernel
- [ ] integrate perf for kernel tracing
- [ ] integrate testing