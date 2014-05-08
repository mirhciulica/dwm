# $Id: PKGBUILD 18861 2010-06-16 09:09:52Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.0
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz \
    config.h
    dwm.desktop
    dwm-6.0-defaultlayout.diff
    dwm-6.0-statuscolors.diff
    dwm-6.0-pertag.diff
    dwm-6.0-systray.diff
    dwm-6.0-tagall.diff)
md5sums=('8bb00d4142259beb11e13473b81c0857'
         '3344d20f4225d3d5be6c0e6bbe18234e'
         '939f403a71b6e85261d09fc3412269ee'
         '8fe7462f59c29ad22a4aaf9807644243'
         'f0c345b547a1b5764fadee390c0ee3c6'
         '54339e932893264d2ee95e134c10d0d4'
         '967174d90cc7d99508f4285fedf301a8'
         'e6d27cc7f20ca67713965d93b36fb853')

build() {
  cd $srcdir/$pkgname-$pkgver
  cp $srcdir/config.h config.h

  patch -Np1 -i $srcdir/dwm-6.0-defaultlayout.diff
  patch -Np1 -i $srcdir/dwm-6.0-statuscolors.diff
  patch -Np1 -i $srcdir/dwm-6.0-pertag.diff
  patch -Np1 -i $srcdir/dwm-6.0-systray.diff
  patch -Np1 -i $srcdir/dwm-6.0-tagall.diff

  sed -i 's/CPPFLAGS =/CPPFLAGS +=/g' config.mk
  sed -i 's/^CFLAGS = -g/#CFLAGS += -g/g' config.mk
  sed -i 's/^#CFLAGS = -std/CFLAGS += -std/g' config.mk
  sed -i 's/^LDFLAGS = -g/#LDFLAGS += -g/g' config.mk
  sed -i 's/^#LDFLAGS = -s/LDFLAGS += -s/g' config.mk
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR=$pkgdir install
  install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
  install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
  install -m644 -D $srcdir/dwm.desktop $pkgdir/usr/share/xsessions/dwm.desktop
}

