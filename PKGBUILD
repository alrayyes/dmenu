# Maintainer: Ryan Kes <alrayyes@gmail.com>

pkgname=dmenu
pkgver=4.9
pkgrel=1
pkgdesc='Generic menu for X'
url='https://tools.suckless.org/dmenu/'
arch=('x86_64')
license=('MIT')
depends=('sh' 'libxinerama' 'libxft' 'freetype2' 'menu-calc' 'pass'  'yubikey-oath-dmenu' 'nerd-fonts-source-code-pro')

sha512sums=('c2779209fe012de8ca1cdd72923da6d594f4a8368c85c3c0e0afd4ae489a95fe0e6f05a947d115b6b389aa7170ab14c2c645a2031353b0a08f38327ab461fe65'
            'a253aff0ec1eb9f2201f7ea624b408e74590bdede9b9eab8240eab80c63dd5be49dcb00629b65704eb185907b90231ea7e6f88a25326ffc8f520fe42b0d8b11a'
            'ad8183cca1ad1dd5b786896f94d127eeea53cece291c485f928388a7589402f49ed7e0ee8bdae71cc2ed41f3276b96591349cd820621f345376a54d557307fdf')

_patches=()

source=(https://dl.suckless.org/tools/dmenu-${pkgver}.tar.gz
    config.h
    dmenu-frequency
    "${_patches[@]}")

prepare() {
  cd ${pkgname}-${pkgver}
  echo "CPPFLAGS+=${CPPFLAGS}" >> config.mk
  echo "CFLAGS+=${CFLAGS}" >> config.mk
  echo "LDFLAGS+=${LDFLAGS}" >> config.mk

  for patch in "${_patches[@]}"; do
    echo "Applying patch $(basename $patch)..."
    patch -Np1 -i "$srcdir/$(basename $patch)"
  done

  cp $srcdir/config.h config.h
}

build() {
  cd ${pkgname}-${pkgver}
  make \
	  X11INC=/usr/include/X11 \
	  X11LIB=/usr/lib/X11 \
	  FREETYPEINC=/usr/include/freetype2
}

package() {
  cd ${pkgname}-${pkgver}
  make PREFIX=/usr DESTDIR="${pkgdir}" install
  install -Dm 644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"

  cd ../
  install -Dm0755 dmenu-frequency "${pkgdir}/usr/bin/dmenu-frequency"
}

# vim: ts=2 sw=2 et:

