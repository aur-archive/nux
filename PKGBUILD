# Maintainer: Charles Bos <charlesbos1 AT gmail>
# Contributor: Balló György <ballogyor+arch at gmail dot com>
# Contributor: Xiao-Long Chen <chenxiaolong@cxl.epac.to>

pkgname=nux
pkgver=4.0.6
pkgrel=1
pkgdesc="Graphical user interface toolkit for applications that mixes OpenGL hardware acceleration with high quality visual rendering"
arch=('i686' 'x86_64')
url="https://launchpad.net/nux"
license=('LGPL')
depends=('gdk-pixbuf2' 'glew' 'pango' 'mesa' 'libsigc++' 'libxcomposite' 'libxdamage' 'libxxf86vm' 'geis' 'ibus')
makedepends=('boost' 'glproto' 'dri2proto' 'doxygen' 'graphviz')
options=('!libtool' '!emptydirs')
source=("http://launchpad.net/$pkgname/4.0/$pkgver/+download/$pkgname-$pkgver.tar.gz"
        '50_check_unity_support'
        '0001_autoconf.patch'
        '01_blacklist_llvmpipe.patch')
md5sums=('e372629eed5aaa4046dd0d10991e9eaa' 
         'c5c000662877c3d5433b2b12e356230b'
         'd88aef172c7c828d388dbc25480ee90b'
         '6df5cea7d441ed4e768e767e9c0b98fe')
install='nux.install'

prepare() {
  cd "$srcdir"/$pkgname-$pkgver

  patch -p1 -i "${srcdir}/0001_autoconf.patch"
  patch -p1 -i "${srcdir}/01_blacklist_llvmpipe.patch"
}

build() {
  cd "$srcdir"/$pkgname-$pkgver

  autoreconf -vfi

  ./configure --prefix=/usr --libexecdir=/usr/lib --disable-static

  make
}

package() {
  cd "$srcdir"/$pkgname-$pkgver

  make DESTDIR="${pkgdir}" install

  rm -rv "${pkgdir}/usr/share/nux/gputests/"

  install -dm755 "${pkgdir}/etc/X11/xinit/xinitrc.d/"
  install -m755 "${srcdir}/50_check_unity_support" \
                "${pkgdir}/etc/X11/xinit/xinitrc.d/"
}
