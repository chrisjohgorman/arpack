# Maintainer: Alexander Rødseth <rodseth@gmail.com>
# Contributor: William Rea <sillywilly@gmail.com>
# Contributor: Stefan Husmann <stefan-husmann@t-online.de>

pkgname=arpack
pkgver=3.1.2
pkgrel=2
arch=('x86_64' 'i686')
pkgdesc='Fortran77 subroutines designed to solve large scale eigenvalue problems'
url='http://forge.scilab.org/index.php/p/arpack-ng/'
license=('BSD')
depends=('lapack' 'openmpi')
provides=('arpack-ng')
source=("http://forge.scilab.org/upload/$pkgname-ng/files/$pkgname-ng_$pkgver.tar.gz")
sha256sums=('9338bda5bef5a4bafd99c18f327acb54f8be4ffc5c53d0a186e4aa27db3260f2')

build() {
  cd "$pkgname-ng_$pkgver"

  ./configure --prefix=/usr --enable-mpi
  make \
    F77="mpif77" \
    CFLAGS+=" `pkg-config --cflags ompi` " \
    LIBS+=" `pkg-config --libs ompi` "
}

package() {
  cd "$pkgname-ng_$pkgver"

  make DESTDIR="$pkgdir/" install
  install -Dm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
}

# vim:set ts=2 sw=2 et:
