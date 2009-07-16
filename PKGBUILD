# $Id: PKGBUILD,v 1.4 2008/07/09 10:01:04 sergej Exp $
# Contributor: William Rea <sillywilly@gmail.com>
pkgname=arpack
pkgver=2.1
pkgrel=3
pkgdesc="A collection of Fortran77 subroutines designed to solve large scale eigenvalue problems"
arch=('i686' 'x86_64')
url="http://www.caam.rice.edu/software/ARPACK"
license=('BSD')
depends=('glibc')
source=(http://www.caam.rice.edu/software/ARPACK/SRC/arpack96.tar.gz \
	http://www.caam.rice.edu/software/ARPACK/SRC/patch.tar.gz \
	arpack-2.1-redhat.patch \
	license.txt)
md5sums=('fffaa970198b285676f4156cebc8626e'
         '14830d758f195f272b8594a493501fa2'
         '95678954de317c92862bb4f9cc9d04ad'
         '7caaa0099a5c39726f4478a1bde89495')

build() {
  cd $startdir/src/ARPACK
  patch -p1 -i ../arpack-2.1-redhat.patch
  mkdir static shared
  cd shared
  for dir in ../SRC ../UTIL; do
    make -f $dir/Makefile VPATH=$dir srcdir=$dir FC=gfortran FFLAGS="-fPIC" \
       single double complex complex16
  done
  gcc -shared -Wl,-soname,libarpack.so.2 -o libarpack.so.2.1 *.o
  cd ..
  cd static
  for dir in ../SRC ../UTIL; do
    make -f $dir/Makefile VPATH=$dir srcdir=$dir FC=gfortran FFLAGS="$RPM_OPT_FLAGS" LDFLAGS="-s" \
       all
  done
  ar rv libarpack.a *.o
  ranlib libarpack.a
  install -d $startdir/pkg/usr/lib
  install -p -m644 $startdir/src/ARPACK/static/libarpack.a $startdir/pkg/usr/lib
  install -p -m755 $startdir/src/ARPACK/shared/libarpack.so.2.1 $startdir/pkg/usr/lib
  ln -s libarpack.so.2.1 $startdir/pkg/usr/lib/libarpack.so.2
  ln -s libarpack.so.2 $startdir/pkg/usr/lib/libarpack.so
  install -D -m644 $startdir/src/license.txt $startdir/pkg/usr/share/licenses/$pkgname/license.txt
}
