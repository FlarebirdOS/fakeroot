pkgname=fakeroot
pkgver=1.37.1.2
pkgrel=3
pkgdesc="Tool for simulating superuser privileges"
arch=('x86_64')
url="https://tracker.debian.org/pkg/fakeroot"
license=('GPL-3.0-or-later')
groups=('base-devel')
depends=(
    'bash'
    'glibc'
    'sed'
    'util-linux'
)
makedepends=('systemd')
install=${pkgname}.install
source=(https://deb.debian.org/debian/pool/main/f/$pkgname/${pkgname}_${pkgver}.orig.tar.gz)
sha256sums=(959496928c8a676ec8377f665ff6a19a707bfad693325f9cc4a4126642f53224)

build() {
    cd ${pkgname}-${pkgver}

    local configure_args=(
        --prefix=/usr
        --libdir=/usr/lib64/libfakeroot
        --disable-static
        --with-ipc=sysv
        --build=${CHOST}
        --host=${CHOST}
    )

    ./configure "${configure_args[@]}"

    make
}

package() {
    cd ${pkgname}-${pkgver}

    make DESTDIR=${pkgdir} install

    install -dm0755 ${pkgdir}/etc/ld.so.conf.d/
    echo '/usr/lib64/libfakeroot' > ${pkgdir}/etc/ld.so.conf.d/fakeroot.conf
}
