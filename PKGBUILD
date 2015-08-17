# Maintainer: Myles English < myles at rockhead dot biz >
# Contributer: Sebastian Eiser
pkgname=scotch_esmumps5
pkgver=5.1.12b
pkgrel=4
pkgdesc="libraries for graph, mesh and hypergraph partitioning, static mapping, and sparse matrix block ordering. This version  contains an interface for MUMPS. The sequential and parallel version are built"
url="http://www.labri.fr/perso/pelegrin/scotch/"
license="CeCILL-C free/libre software license"
depends=('zlib' 'openmpi')
provides=('ptscotch=5.1.12b' 'scotch=5.1.12b')
conflicts=('ptscotch' 'scotch' 'ptscotch-openmpi' 'ptscotch-mpich2' 'scotch_esmumps')
arch=('i686' 'x86_64')
source=("https://gforge.inria.fr/frs/download.php/28978/scotch_${pkgver}_esmumps.tar.gz")
options=('!makeflags')

_pkgver=5.1.12

build() {
  cd "${srcdir}/scotch_${_pkgver}_esmumps"/src

  [ -e Makefile.inc ] && rm Makefile.inc
  cp Make.inc/Makefile.inc.i686_pc_linux2.shlib Makefile.inc
  sed -i "s|-O3|${CFLAGS}|g" Makefile.inc

  make scotch
  make ptscotch
  make esmumps
}

package() {
  cd "${srcdir}/scotch_${_pkgver}_esmumps/src"

  mkdir ${pkgdir}/usr
  make install prefix=${pkgdir}/usr

  install -m 644 "${srcdir}/scotch_${_pkgver}_esmumps/lib/libesmumps.so" \
      "${srcdir}/scotch_${_pkgver}_esmumps/lib/libptesmumps.so" ${pkgdir}/usr/lib/

  install -d -m 755 ${pkgdir}/usr/include/scotch
  mv ${pkgdir}/usr/include/*.h ${pkgdir}/usr/include/scotch
  install -m 644 "${srcdir}/scotch_${_pkgver}_esmumps/include/esmumps.h" \
      ${pkgdir}/usr/include/scotch
      
  install -m 644 -D "${srcdir}/scotch_${_pkgver}_esmumps/doc/CeCILL-C_V1-en.txt" \
      "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
md5sums=('e13b49be804755470b159d7052764dc0')
