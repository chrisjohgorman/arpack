# Maintainer: Alexander F Rødseth <xyproto@archlinux.org>
# Contributor: William Rea <sillywilly@gmail.com>
# Contributor: Stefan Husmann <stefan-husmann@t-online.de>

pkgname=arpack
pkgver=3.3.0
pkgrel=2
arch=('x86_64' 'i686')
pkgdesc='Fortran77 subroutines designed to solve large scale eigenvalue problems'
url='https://github.com/opencollab/arpack-ng'
license=('BSD')
depends=('lapack' 'openmpi')
makedepends=('git' 'gcc-fortran' 'openmpi')
provides=('arpack-ng')
source=("git://github.com/opencollab/arpack-ng#tag=$pkgver")
md5sums=('SKIP')

prepare() {
  cd "$pkgname-ng"

  ./bootstrap
}

build() {
  cd "$pkgname-ng"

  ./configure --prefix=/usr --enable-mpi
  make \
    F77="mpif77" \
    CFLAGS+=" `pkg-config --cflags ompi-f77` " \
    LIBS+=" `pkg-config --libs ompi-f77` "
}

package() {
  cd "$pkgname-ng"

  make DESTDIR="$pkgdir" install
  install -Dm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
}

# vim:set ts=2 sw=2 et:
