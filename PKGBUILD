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
    dwm-columns-6.0-cy.diff
    dwm-pertag-6.1.diff
    dwm-systray-6.1-cy.diff
    cy.diff
	dwm.desktop)
sha256sums=('c2f6c56167f0acdbe3dc37cca9c1a19260c040f2d4800e3529a21ad7cce275fe'
            '76cd5bcd8acd17cd5dc91762afac7211ab253b720aa746613ad10e1c95465566'
            'c5a3a1aa21d6538700d04faba2d73c55d92d6009e7d7be60556c8bd0d7ba5614'
            'fb7d9b75e0fb0e1214124ff0839e4e505d0b82cbe1d6c231e91011103eb7b469'
            'ab0058b17f33e65ebc08cec17ede0564bcdae0e9483f59f0d0158703fba5cb0b'
            '7163f49edecc0f50e39060f24e7947083300b3820621b1fc11d8fe4fcbaeae19'
            'bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81')

prepare() {
  cd $srcdir/$pkgname-$pkgver
  cp $srcdir/config.h config.h
}

build() {
  cd $srcdir/$pkgname-$pkgver

  # Apply columns patch
  patch -p1 -i "${srcdir}/dwm-columns-6.0-cy.diff"

  # Apply pertag patch
  patch -p1 -i "${srcdir}/dwm-pertag-6.1.diff"

  # Apply systray patch
  patch -p1 -i "${srcdir}/dwm-systray-6.1-cy.diff"

  # Apply cy patch
  patch -p1 -i "${srcdir}/cy.diff"

  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR=$pkgdir install
  install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
  install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
  install -m644 -D $srcdir/dwm.desktop $pkgdir/usr/share/xsessions/dwm.desktop
}
