# Maintainer: Ryan Kes <alrayyes@gmail.com>

pkgname=dmenu
pkgver=4.9
pkgrel=1
pkgdesc='Generic menu for X'
url='https://tools.suckless.org/dmenu/'
arch=('x86_64')
license=('MIT')
depends=('sh' 'libxinerama' 'libxft' 'freetype2' 'menu-calc' 'pass'  'yubikey-oath-dmenu' 'otf-nerd-fonts-fira-code')

sha512sums=('c2779209fe012de8ca1cdd72923da6d594f4a8368c85c3c0e0afd4ae489a95fe0e6f05a947d115b6b389aa7170ab14c2c645a2031353b0a08f38327ab461fe65'
            'e2aefad0eb1d7abd31ed359d62687096b1657bb47bae963ff7626c7b0f5da40ce3dccc154234f9f785e02d518fde9dc4843f8a02030a393c5e0188066ff459e5')

_patches=()

source=(https://dl.suckless.org/tools/dmenu-${pkgver}.tar.gz
    config.h
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
}

# vim: ts=2 sw=2 et:

