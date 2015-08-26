# Maintainer: Alexander F Rødseth <rodseth@gmail.com>
# Contributor: William Rea <sillywilly@gmail.com>
# Contributor: Stefan Husmann <stefan-husmann@t-online.de>

pkgname=arpack
pkgver=3.2.0
pkgrel=2
arch=('x86_64' 'i686')
pkgdesc='Fortran77 subroutines designed to solve large scale eigenvalue problems'
url='https://github.com/opencollab/arpack-ng'
license=('BSD')
depends=('lapack' 'openmpi')
makedepends=('openmpi' 'gcc-fortran' 'git')
provides=('arpack-ng')
source=("git://github.com/opencollab/arpack-ng#tag=$pkgver")
md5sums=('SKIP')

build() {
  cd "$pkgname-ng"

  ./configure --prefix=/usr --enable-mpi
  make \
    F77="mpif77" \
    CFLAGS+=" `pkg-config --cflags ompi` " \
    LIBS+=" `pkg-config --libs ompi` "
}

package() {
  cd "$pkgname-ng"

  make DESTDIR="$pkgdir" install
  install -Dm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
}

# getver ok
# vim:set ts=2 sw=2 et:
