# Maintainer: Ryan Kes <alrayyes@gmail.com>

pkgname=dmenu
pkgver=5.0
pkgrel=1
pkgdesc='Generic menu for X'
url='https://tools.suckless.org/dmenu/'
arch=('x86_64')
license=('MIT')
depends=('sh' 'libxinerama' 'libxft' 'freetype2' 'menu-calc' 'pass'  'yubikey-oath-dmenu' 'otf-nerd-fonts-fira-code')

sha512sums=('2b6a7cdf5aefc5e7ca7a4944883c3c16ee6f5005d2a96b61482d4899ad395f9cb8926907681d88b9df3e1188cf421dad4cc17e343b752f6cb8b161d33384b3f3'
            'e2aefad0eb1d7abd31ed359d62687096b1657bb47bae963ff7626c7b0f5da40ce3dccc154234f9f785e02d518fde9dc4843f8a02030a393c5e0188066ff459e5'
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

