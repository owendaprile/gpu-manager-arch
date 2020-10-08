# gpu-manager-arch

A fork of Ubuntu's gpu-manager modified to work with Arch Linux.

## Why make this?
On it's own, gpu-manager doesn't do very much. It is useful
in combination with other tools built into Ubuntu such as
`prime-select` which will switch between graphics modes. 
However, [system76-power](https://github.com/pop-os/system76-power)
relies on gpu-manager to modify the X11 configuration files
when swiching graphics modes. I wanted system76-power to
work correctly on Arch so I could change graphics modes
from the [extension](https://github.com/pop-os/gnome-shell-extension-system76-power).

## What does it do?
What I've gathered from modifying it is that it reads the file
`/etc/prime-discrete` and writes configuration files to 
`/usr/share/X11/xorg.conf.d/`, mainly setting `PrimaryGPU` to
`yes` or `no`. It has many more features, but I'm not sure
what they're for as I only have an Intel/Nvidia system and
can't see the rest of it working.

## How can I use it?
I'm writing a post on how to get `system76-power` working with
the extension so power and graphics modes can be switched just
like on Pop!_OS.

## Building
Use the provided PKGBUILD or just run `make`.

## Contributing
I only have an XPS 15 with Intel integrated graphics and a 
discrete Nvidia card. I can't test on other systems so I don't 
know how it works on other configurations. I've gone through the
code and modified many of the Ubuntu specific parts, but I've
probably missed something, especially relating to other hardware
setups. I haven't noticed any issues, but if you do, feel free to
open an issue or try to fix it yourself.

## What did I modify?
Not very much. I had to change quite a few paths that were Ubuntu
specific such as kernel module directories and other configuration
directories. I also had to remove a section which used `dpkg` to
find the architecture of the kernel, which I don't think Arch does
at all. The service file relied on the `oem-config` service and 
target which is Ubuntu specific. I modified the service file to
start up before `multi-user.target`, which seems to work, but I'm
not sure what target should be used to ensure it starts before
the X server. Some install paths were modified from the Ubuntu
package, but end up in the same place to minimize modification
of the source code.