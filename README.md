# v4l2-relayd-intel-mipi

This is an alternative, and easier, solution to [my original repository](https://github.com/oznakn/arch-ov08x40/) of making Intel MIPI cameras work with Linux kernel, for my Lenovo Thinkpad X1 Carbon gen 12.

With Linux kernel version 6.18 and latest updates, only installing this repository should be enough to make the camera work.

## Requirements

- Linux `v6.18+`

## How to install

- Run `yay -Bi .`
- During installation, select `intel-ipu6-camera-hal-git` if an alternative is provided.
- Run `sudo systemctl enable v4l2-relayd@virtual-camera`
- Then reboot

## How to test

- Run `gst-launch-1.0 icamerasrc ! autovideosink`. The camera should be working.
