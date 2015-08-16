pkgname=libftdi1
true && pkgname=('libftdi1' 'python-libftdi1')
pkgbase=libftdi1
pkgver=1.0
pkgrel=2
license=('GPL2' 'LGPL2.1')
arch=('i686' 'x86_64')
url='http://www.intra2net.com/en/developer/libftdi/'
makedepends=('libusbx' 'boost' 'cmake' 'gcc' 'python' 'swig' 'doxygen' 'confuse')
source=(http://www.intra2net.com/en/developer/libftdi/download/$pkgbase-$pkgver.tar.bz2)
sha1sums=('5be76cfd7cd36c5291054638f7caf4137303386f')

build() {
  cd $pkgbase-$pkgver
  sed -i "s|NOT LIB_SUFFIX|NOT DEFINED LIB_SUFFIX|g" CMakeLists.txt
  cmake . -DCMAKE_INSTALL_PREFIX=/usr \
          -DLIB_SUFFIX="" \
          -DCMAKE_SKIP_RPATH=ON
  make
}

check() {
  cd $pkgbase-$pkgver
  make check || return 0
}

package_libftdi1() {
  pkgdesc='Library to talk to FTDI chips'
  depends=('libusbx' 'confuse' 'gcc-libs')

  cd $pkgbase-$pkgver
  make DESTDIR="$pkgdir" install -C src
  make DESTDIR="$pkgdir" install -C ftdipp
  make DESTDIR="$pkgdir" install -C ftdi_eeprom
  make DESTDIR="$pkgdir" install/local
}

package_python-libftdi1() {
  pkgdesc='Python bindings for LibFTDI'
  depends=("$pkgbase" 'python')

  cd $pkgbase-$pkgver
  make DESTDIR="$pkgdir" install -C bindings
}

pkgdesc='Library to talk to FTDI chips'
