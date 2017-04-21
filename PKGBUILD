# $Id: PKGBUILD 60970 2011-12-19 21:33:58Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.0
pkgrel=99
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
	config.h
    xft.patch
    dwm-r1580-col.diff
    dwm-6.0-pertag.diff
    dwm-6.0cy-systray.diff
	dwm.desktop)
md5sums=('8bb00d4142259beb11e13473b81c0857'
         '354348307a8ed85da8ccd562245fedad'
         'd2cdac3711f5eee49927615ed9c68479'
         '885a21848de52d1e24d8c660f5e05892'
         '613a6e64285c4748c9db1179fc4ab498'
         'd82884c7a96a2ea37cb65abe073aa11c'
         '939f403a71b6e85261d09fc3412269ee')

build() {
  cd $srcdir/$pkgname-$pkgver

  # Apply pertag patch
  patch -p1 -i "${srcdir}/dwm-6.0-pertag.diff"

  # Apply columns patch
  patch -p1 -i "${srcdir}/dwm-r1580-col.diff"

  # Apply patch for XFT support
  patch -p1 -i "${srcdir}/xft.patch"

  # Apply systray patch
  patch -p1 -i "${srcdir}/dwm-6.0cy-systray.diff"

  cp $srcdir/config.h config.h
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
