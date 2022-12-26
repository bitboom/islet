# ISLET
ISLET is a project to enable on-device confidential computing
for end users by leveraging ARMv9 CCA that is
the newly emerging confidential computing hardware on ARM devices.
Using the hardware support, ISLET enables a Trusted Execution Environment (TEE)
on user’s devices within which users can securely process, store, communicate
and manage their private data. The protection provided by
ISLET applies not only to data-at-rest but also to data-in-use
even in the presence of malicious privileged software on devices.

We develop components enabling Realm Virtual Machines (VMs),
which are secure VM-level TEE provided by ARMv9 CCA.
To manage Realm VMs, Realm Management Monitor (RMM)
is needed to be running at EL2 in the Realm world.
ISLET provides the implementation of RMM that is written in Rust. 

## Getting started 
### Installing dependencies
```bash
./scripts/init.sh
```

### Running linux as a realm
```bash
// Start FVP
$ ./scripts/fvp-cca --normal-world=linux --realm-vm=linux

// Login with root in the normal world linux
Welcome to Buildroot, type root or test to login
buildroot login: root

// Run a linux realm
# cd /qemu/guest/
# ../qemu-system-aarch64 \
        -kernel Image_realmvm \
        -initrd initramfs-busybox-aarch64.cpio.gz \
        -append "earlycon=pl011,mmio,0x1c0a0000 console=ttyAMA0" \
        --enable-kvm \
        -cpu host \
        -smp 1 \
        -M virt,gic-version=3 \
        -m 256M \
        -nographic
```

### Testing islet-rmm with tf-a-tests
```
$ ./scripts/fvp-cca --normal-world=tf-a-tests
```
