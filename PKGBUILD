# Maintainer: Olof Sandell <olof.sandell@protonmail.com>
# Original Maintainer: Vincent Grande <shoober420@gmail.com>
# Contributor: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Jan de Groot

pkgname=libinput-accel-smooth-git
pkgver=1.23.0.r27.g3d6a4709
pkgrel=1
pkgdesc="Input device management and event handling library (Personal build with smooth acceleration)"
url="https://www.freedesktop.org/wiki/Software/libinput/"
arch=(x86_64)
license=(custom:X11)
depends=('mtdev' 'libevdev' 'libwacom')
provides=('libinput')
conflicts=('libinput')
# upstream doesn't recommend building docs
makedepends=('gtk3' 'meson') # 'doxygen' 'python-sphinx' 'python-recommonmark'
optdepends=('gtk3: libinput debug-gui'
            'python-pyudev: libinput measure'
            'python-evdev: libinput measure'
            'xorg-xinput: input configuration for X')
source=(git+https://github.com/osandell/libinput-accel-smooth.git#branch=feature/smooth-acceleration)

sha512sums=('SKIP')
validpgpkeys=('SKIP') # Peter Hutterer (Who-T) <office@who-t.net>

pkgver() {
	cd libinput-accel-smooth
	git describe --long | sed -r 's/([^-]*-g)/r\1/;s/-/./g'
}

build() {
  arch-meson libinput-accel-smooth build \
    -Dudev-dir=/usr/lib/udev \
    -Dtests=false \
    -Ddocumentation=false
  ninja $NINJAFLAGS -C build
}

package() {
  DESTDIR="$pkgdir" ninja $NINJAFLAGS -C build install

  install -Dvm644 libinput-accel-smooth/COPYING \
    "$pkgdir/usr/share/licenses/libinput/LICENSE"
}
