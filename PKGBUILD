# Maintainer: Alexander Rødseth <rodseth@gmail.com>
# Contributor: William Rea <sillywilly@gmail.com>
# Contributor: Stefan Husmann <stefan-husmann@t-online.de>
pkgname=arpack
pkgver=3.0.2
pkgrel=1
pkgdesc="Collection of Fortran77 subroutines designed to solve large scale eigenvalue problems"
arch=('x86_64' 'i686')
provides=('arpack-ng')
options=(!libtool)
url="http://forge.scilab.org/index.php/p/arpack-ng/"
license=('BSD')
depends=('glibc' 'gcc-fortran' 'lapack')
source=("http://forge.scilab.org/upload/arpack-ng/files/arpack_3.0.2.tar.gz")
sha256sums=('4add769386e0f6b0484491bcff129c6f5234190dbf58e07cc068fbd5dc7278bf')

build() {
  cd "$srcdir/$pkgname-ng-$pkgver"

  ./configure --prefix=/usr
  make
}

package() {
  cd "$srcdir/$pkgname-ng-$pkgver"

  make DESTDIR="$pkgdir/" install
  install -Dm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
}

# vim:set ts=2 sw=2 et:
