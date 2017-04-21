# $Id: PKGBUILD 165985 2016-03-10 18:31:18Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.1
pkgrel=3
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'st' 'dmenu')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
	config.h
    columns.diff
    pertag.diff
    systray.diff
    config.mk.diff
	dwm.desktop)
sha256sums=('c2f6c56167f0acdbe3dc37cca9c1a19260c040f2d4800e3529a21ad7cce275fe'
            '76cd5bcd8acd17cd5dc91762afac7211ab253b720aa746613ad10e1c95465566'
            '2a27f4ced451924809003d0c7e411f2b710fda41387846b16001e94ca51f0ac8'
            '3ba85c636b0720b38b16c393b25759cee5a479c15084faefc7cc5318725265af'
            'ed07fab9b80fd01a28757a4ed987e5d3e323b18cd0235ce278e199a83f3253fe'
            'df9872493889fbac009b35539b3efd4fdf86e162e409e8fb03a0648cd19e3b4f'
            'bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81')

prepare() {
  cd $srcdir/$pkgname-$pkgver
  cp $srcdir/config.h config.h
}

build() {
  cd $srcdir/$pkgname-$pkgver

  # Apply columns patch
  patch -p1 -i "${srcdir}/columns.diff"

  # Apply pertag patch
  patch -p1 -i "${srcdir}/pertag.diff"

  # Apply systray patch
  patch -p1 -i "${srcdir}/systray.diff"

  # Apply cy patch
  patch -p1 -i "${srcdir}/config.mk.diff"

  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR=$pkgdir install
  install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
  install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
  install -m644 -D $srcdir/dwm.desktop $pkgdir/usr/share/xsessions/dwm.desktop
}
