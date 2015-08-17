# Maintainer: Pawel 'l0ner' Soltys <pwslts@gmail.com>
# Contributor: Calvin Morrison <mutantturkey@gmail.com>

pkgname=trinity-dbus-tqt
pkgver=3513
pkgrel=3
arch=('i686' 'x86_64')
url='http://www.trinitydesktop.org'
license=('GPL')
groups=('trinity-base')
pkgdesc="Trinity TQt DBus wrapper"
depends=('trinity-arts' 'dbus-core')
makedepends=('pkgconfig' 'cmake')
options=('libtool' '!strip')
source=(http://mirror.ets.kth.se/trinity/releases/3.5.13/dependencies/dbus-tqt-3.5.13.tar.gz)
md5sums=('46ae165c068271485c827f6fc6687a9a')
install='trinity-dbus-tqt.install'

build() {
   msg "Setting PATH, CMAKE and Trinity Environment variables"
   # Source the QT and TDE profile
   [ "$QTDIR" = "" ] && . /etc/profile.d/qt3.sh 
   [ "$TDEDIR" = "" ] && . /etc/profile.d/trinity.sh

   #export CMAKE_PREFIX_PATH=${QTDIR}:${TDEDIR}
   #export CMAKE_INCLUDE_PATH=/usr/include/dbus-1.0:${TDEDIR}/include:${TDEDIR}/include/libkrandr
   #export LD_LIBRARY_PATH=${TDEDIR}/lib:${TDEDIR}/lib/trinity:$LD_LIBRARY_PATH
   #export PKG_CONFIG_PATH=${TDEDIR}/lib/pkgconfig:${QTDIR}/lib/pkgconfig

   cd $srcdir
   msg "Creating out-of-source build directory: ${srcdir}/build"
   mkdir -p build
   cd build

   msg "Starting cmake..."
   cmake ${srcdir}/dependencies/dbus-tqt \
      -DCMAKE_INSTALL_PREFIX=$TDEDIR 

   msg "Building - $pkgname..."
   make
}

package() {
   msg "Packaging - $pkgname-$pkgver"
   cd ${srcdir}/build
   make DESTDIR="${pkgdir}" install
}
