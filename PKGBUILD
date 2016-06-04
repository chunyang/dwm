# Maintainer: Chun Yang <x@cyang.info>

pkgname=dwm-cy
pkgver=6.1
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'rxvt-unicode' 'dmenu')
source=(config.h
        drw.c
        drw.h
        dwm.c
        transient.c
        util.c
        util.h
        Makefile
        config.mk
        dwm.1
        dwm.png
        LICENSE
        README)

build() {
    cd $srcdir
    make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
    cd $srcdir
    make PREFIX=/usr DESTDIR=$pkgdir install
    install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
    install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
}
