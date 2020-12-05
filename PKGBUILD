# Maintainer: Ryan Kes <ryan@ryankes.eu>

pkgname=dmenu
pkgver=5.0
pkgrel=1
pkgdesc='Generic menu for X'
url='https://tools.suckless.org/dmenu/'
arch=('x86_64')
license=('MIT')
depends=('sh' 'glibc' 'coreutils' 'libx11' 'libxinerama' 'freetype2' 'fontconfig' 'libfontconfig.so' 'menu-calc' 'pass' 'yubikey-oath-dmenu')

sha512sums=('2b6a7cdf5aefc5e7ca7a4944883c3c16ee6f5005d2a96b61482d4899ad395f9cb8926907681d88b9df3e1188cf421dad4cc17e343b752f6cb8b161d33384b3f3'
            'f2f1c94b5d39d23b99d0832450e820b7652e9e3e3a591c473b3e0edbd895b75d5b056b5723d7321b1026f76b599e2f5b53d3bb41a7527c7871c9628594293d2c'
            'beed0f7725d84b4d73cb35fb7d78d7db90c7fa15ed0ac4d6cf19e6469caf83167bc3edae246c30a2f0a79e765b46d9a37997a9a72f5dec147cc0a904fa2ef790'
            'ce806c6481b20d5b2352fc387816878c75285162f6404b3a969a95f9dbd6c7476fd4c6571f260886fa30ccc40e4a388ea8f6902e40ff90447e04bec3faf0669d'
            '6ce4ce0ddb9c1058f253ce46cdae8949c468d97ce7d787831d8a4f4ebd4db672761e2552703f58d36d01b2933dea624a30627629027b9a5960b404542a40a732'
            'e6ff377a4a4ed9e98d05a8870d6c57a5f89f853b0ec1160c3702642f899d8079eca595775b3d9f436bd67626fd4df659e511faa6d026130b07eef09a7c0c8b85'
            '15d88ea4f10c2fa6fb3eb7478f23b24210a0da3542ae7a5be609013500c15564eedd8153d850f079c2c1f4bab1f5e61ff51153e4c85445ee04a0de5c851e305a'
            'fe0167c56ca9381928b5dd20383d36554729fb5417bf42f0db2e1634a1f82774f068cbea347e68c6cb3adc6c1a5f97ab263c8a9450f0b2c6429ac66de3edf894')

_patches=(
    "dmenu-border-4.9.diff"
    "dmenu-fuzzyhighlight-4.9.diff"
    "dmenu-fuzzymatch-4.9.diff"
    "local-dmenu-mousesupport-5.0.diff"
    "dmenu-numbers-4.9.diff"
    "local-allow-color-fonts.diff"
)

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
