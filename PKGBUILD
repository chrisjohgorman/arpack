# Maintainer: Alexander Rødseth <rodseth@gmail.com>
# Contributor: William Rea <sillywilly@gmail.com>
# Contributor: Stefan Husmann <stefan-husmann@t-online.de>

pkgname=arpack
pkgver=3.1.0
pkgrel=2
arch=('x86_64' 'i686')
pkgdesc="Fortran77 subroutines designed to solve large scale eigenvalue problems"
url="http://forge.scilab.org/index.php/p/arpack-ng/"
license=('BSD')
depends=('glibc' 'gcc-fortran' 'lapack' 'openmpi>=1.5.4-4')
provides=('arpack-ng')
options=('!libtool')
source=("http://forge.scilab.org/upload/$pkgname-ng/files/$pkgname-ng_$pkgver.tar.gz")
sha256sums=('65b7856126f06ecbf9ec450d50df92ca9260d4b0d21baf02497554ac230d6feb')

build() {
  cd "$srcdir/$pkgname-ng_$pkgver"

  ./configure --prefix=/usr --enable-mpi
  make F77="gfortran" LIBS+=" `pkg-config --libs ompi` "
}

package() {
  cd "$srcdir/$pkgname-ng_$pkgver"

  make DESTDIR="$pkgdir/" install
  install -Dm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
}

# vim:set ts=2 sw=2 et:
