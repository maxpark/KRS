# Kria Robotics Stack (KRS)

```eval_rst
.. sidebar:: Before you begin

   KRS builds on ROS 2.

   If you're not familiar with it, before continuing, learn more about ROS 2 from its `official documentation <https://docs.ros.org/>`_.
```

The **Kria Robotics Stack (KRS)** is a ROS 2 superset for industry, an integrated set of robot libraries and utilities to accelerate the development, maintenance and commercialization of industrial-grade robotic solutions while using [adaptive computing](https://www.xilinx.com/applications/adaptive-computing.html). KRS provides to ROS 2 users an easy and robust path to hardware acceleration. It allow ROS 2 roboticists to create custom secure compute architectures with higher productivity. KRS leverages Xilinx technology targeting the [Kria SOM portfolio](https://www.xilinx.com/products/som/kria.html) to deliver low latency (real-fast), determinism (predictable), real-time (on-time), security and high throughput to robotics.

It does so by tightly integrating itself with ROS (lingua franca amongst roboticists) and by leveraging a combination of modern C++ and High-Level Synthesis (HLS), together with reference development boards and design architectures roboticists can use to kick-start their projects. Altogether, KRS supports Kria SOMs with an accelerated path to production in robotics.



```eval_rst
.. admonition:: Alpha Release

    KRS **alpha** release documentation is available at https://github.com/vmayoral/KRS/tree/krs-alpha. 


.. admonition:: Beta Release
    
    KRS is on **beta** release. Correspondingly, the documentation provided here is not intended for production environments and should be used only for evaluation purposes.

    *Stay tuned for upcoming official releases*.
```

![](imgs/krs.svg)


</br>
</br>

## KRS capabilities

<style>
table th:first-of-type {
    width: 15%;
}
table th:nth-of-type(2) {
    width: 30%;
}
table th:nth-of-type(3) {
    width: 55%;
}

.wy-table-responsive table td,
.wy-table-responsive table th {
    white-space: normal;
}
</style>

| action | quick peek | description |
|--------|-------------|------------|
| *install KRS* | [![asciicast](https://asciinema.org/a/434953.svg)](https://asciinema.org/a/434953) | Installing KRS is just about creating a ROS 2 workspace, fetching the `krs.repos` of the corresponding release (e.g. [alpha release](https://github.com/vmayoral/KRS/releases/tag/alpha)) and built it using the common ROS flow, with the option of leveraging ament and colcon extensions for additional hardware acceleration capabilities. |
| `select` | [![asciicast](https://asciinema.org/a/434781.svg)](https://asciinema.org/a/434781) | The `select` verb allows to easily select and configure a specific target firmware for hardware acceleration, and default to it while producing binaries and accelerators.  |
| `list` | [![asciicast](https://asciinema.org/a/434781.svg)](https://asciinema.org/a/434781) | The `list` verb  allows to inspect the acceleration firmware available in the ROS workspace, marking with a `*` the currently selected option.  |
| `linux` | [![asciicast](https://asciinema.org/a/scOognokU4wt0PW3E1N4F0jCe.svg)](https://asciinema.org/a/scOognokU4wt0PW3E1N4F0jCe) | The `linux` verb helps configure the Linux kernel in the raw SD card image produced by the firmware. E.g. `colcon acceleration linux vanilla` will produce a Linux vanilla kernel, whereas `colcon acceleration linux preempt_rt` will instead use a pre-built kernel and kernel modules for improved determinism (fully preemptible kernel). |
| `hypervisor`   |  [![asciicast](https://asciinema.org/a/443406.svg)](https://asciinema.org/a/443406) | The `hypervisor` verb helps configure the [Xen](https://xenproject.org/) hypervisor in the raw SD card image produced by the firmware. E.g. `colcon acceleration hypervisor --dom0 vanilla --domU vanilla --dom0less preempt_rt` will produce a raw image leveraging Xen with 3 VMs. The first, `dom0`, uses a vanilla  kernel. The second, `domU`, uses a vanilla kernel. The third is a   `dom0less` VM and uses a fully preemtible kernel   (*preemt_rt*). Unless otherwise specified, all VMs use  the default ROS 2 configuration, PetaLinux-based  rootfs, the LNS and an Ethernet link layer. |
| `emulation`   | [![asciicast](https://asciinema.org/a/443408.svg)](https://asciinema.org/a/443408)  | The `emulation` verb helps manage the emulation capabilities with [QEMU](https://www.qemu.org/) open source machine emulator and virtualizer. This way, developers can test their setups and algorithms without the hardware, which facilitates testing and speeds up the development process allowing for CI/CD pipelines.  Emulation boots the same SD card image produced by previous commands and including the ROS 2 development workspace, providing a unified development approach. |
| `platform`  | [![asciicast](https://asciinema.org/a/443410.svg)](https://asciinema.org/a/443410)  | The `platform` verb helps reports Vitis platform enabled in the firmware deployed in the ROS 2 workspace.  |
| `mkinitramfs`  | [![asciicast](https://asciinema.org/a/443412.svg)](https://asciinema.org/a/443412)  | The `mkinitramfs` verb creates compressed cpio initramfs (ramdisks). These can then be used to back up the current rootfs or to create dom0less VMs in Xen easily.  |
| `mount` / `umount`  | [![asciicast](https://asciinema.org/a/443414.svg)](https://asciinema.org/a/443414)  | The `mount` and `umount` verbs help mount/umount the raw SD card image produced by previous steps. This way, developers can easily access the embedded rootfs directly, across the various partitions of the raw image (e.g. as in the case of multi-VMs in Xen).  |
