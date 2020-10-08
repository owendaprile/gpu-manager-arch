pkgname=gpu-manager-arch
pkgver=0.8.1
pkgrel=1
pkgdesc="Modified version of Ubuntu's gpu-manager that works with Arch"
arch=('x86_64')
url='https://launchpad.net/ubuntu/+source/ubuntu-drivers-common'
license=('GPL2')
# Not sure what is required just for running and just for building.
# depends=('')
# makedepends=('')
source=('git+https://github.com/owendaprile/gpu-manager-arch.git')
sha256sums=('SKIP')

build() {
    cd ${pkgname}
    make
}

package() {
    cd ${pkgname}
    install -Dm755 gpu-manager ${pkgdir}/usr/bin/gpu-manager
    install -Dm644 gpu-manager.service ${pkgdir}/usr/lib/systemd/system/gpu-manager.service
    install -Dm644 71-u-d-c-gpu-detection.rules ${pkgdir}/usr/lib/udev/rules.d/71-u-d-c-gpu-detection.rules
    install -Dm644 u-d-c-print-pci-ids ${pkgdir}/usr/bin/u-d-c-print-pci-ids
    install -Dm644 gpu-manager.target ${pkgdir}/usr/lib/systemd/system/gpu-manager.target
}