# Maintainer: Alexander F. Rødseth <xyproto@archlinux.org>
# Contributor: William Rea <sillywilly@gmail.com>
# Contributor: Stefan Husmann <stefan-husmann@t-online.de>

pkgname=arpack
pkgver=3.6.2
pkgrel=1
arch=('x86_64')
pkgdesc='Fortran77 subroutines for solving large scale eigenvalue problems'
url='https://github.com/opencollab/arpack-ng'
license=('BSD')
depends=('lapack' 'openmpi')
makedepends=('gcc-fortran' 'git')
provides=('arpack-ng')
source=("git+https://github.com/opencollab/arpack-ng#tag=$pkgver")
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

# vim: ts=2 sw=2 et:
