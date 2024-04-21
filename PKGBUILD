# Maintainer: Alexander F. Rødseth <xyproto@archlinux.org>
# Contributor: William Rea <sillywilly@gmail.com>
# Contributor: Stefan Husmann <stefan-husmann@t-online.de>
# Contrubutor: Chris Gorman <chrisjohgorman@gmail.com>

pkgname=arpack64
_pkgname=arpack
pkgver=3.9.1
pkgrel=2
arch=(x86_64)
pkgdesc='Fortran77 subroutines for solving large scale eigenvalue problems (64 bit version)'
url='https://github.com/opencollab/arpack-ng'
license=(BSD)
depends=(lapack openmpi)
makedepends=(gcc-fortran git)
provides=(arpack-ng)
source=("git+$url#commit=40329031ae8deb7c1e26baf8353fa384fc37c251") # tag: 3.9.1
b2sums=('SKIP')

prepare() {
  cd $_pkgname-ng
  ./bootstrap
}

build() {
  cd $_pkgname-ng
  FFLAGS="-fdefault-integer-8" LIBSUFFIX="64" ./configure --enable-icb --enable-mpi --prefix=/usr --with-blas=/usr/lib/libblas64.so --with-lapack=/usr/lib/liblapack64.so
  make F77=mpif77 \
    CFLAGS+=" $(pkg-config --cflags ompi-f77) " \
    LIBS+=" $(pkg-config --libs ompi-f77) "
}

package() {
  cd $_pkgname-ng
  make DESTDIR="$pkgdir" install
  install -Dm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
  cd "$pkgdir"/usr/include
  mv arpack arpack64
}
