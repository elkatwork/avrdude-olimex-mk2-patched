# Maintainer: Samuel Ace Winchenbach <swinchen at gmail dot com>
pkgname=avrdude-svn
_pkgname=avrdude
pkgrel=1
pkgver=20211114.1476
pkgdesc="AVRDUDE is an utility to download/upload/manipulate the ROM and EEPROM contents of AVR microcontrollers using the in-system programming technique (ISP)."
arch=(i686 x86_64 armv6h armv7h)
url="http://www.nongnu.org/avrdude/"
license=('GPL')
groups=()
depends=('libftdi' 'libusb-compat' 'hidapi')
makedepends=(svn)
optdepends=('elfutils')
provides=('avrdude')
conflicts=('avrdude' 'avrdude-osuisp2-svn')
replaces=()
backup=()
options=()
install=
changelog=
source=("${pkgname}::svn+http://svn.savannah.nongnu.org/svn/avrdude/trunk"
        "https://www.olimex.com/Products/AVR/Programmers/AVR-ISP-MK2/resources/endpointdetect_pass1.patch")
noextract=()
md5sums=('SKIP'
         '8cb7fd8745d5d6534a48d6b19f375e4b')

prepare() {
  cd "${srcdir}/${pkgname}/${_pkgname}"
  patch --forward --input="${srcdir}/endpointdetect_pass1.patch"
}

build() {
  cd "${srcdir}/${pkgname}/${_pkgname}"
  ./bootstrap
  ./configure --mandir=/usr/share/man \
    --prefix=/usr \
    --sysconfdir=/etc \
    --enable-linuxgpio
  make
}

package() {
  cd "${srcdir}/${pkgname}/${_pkgname}"

  make DESTDIR="${pkgdir}/" install
}

pkgver() {
  cd "${srcdir}/${pkgname}"
  svn info | awk '/Revision/{r=$2}/Date/{gsub(/-/,"");d=$4}END{print d"."r}'
}
