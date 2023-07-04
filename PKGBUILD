# Maintainer: Balló György <ballogyor+arch at gmail dot com>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Unknown47 <unknown47r@gmail.com>
# Contributor: Angel Velasquez <angvp@archlinux.org>
# Contributor: Juergen Hoetzel <juergen@archlinux.org>

pkgname=libfm
provides=(libfm-extra libfm-gtk2)
conflicts=(libfm-extra libfm-gtk2 libfm-gtk3)
pkgver=1.3.2
pkgrel=1
pkgdesc='Library for file management'
url='https://lxde.org/'
arch=('x86_64')
license=('GPL')
depends=('gtk2' 'libexif' 'menu-cache')
makedepends=('intltool' 'gtk-doc' 'vala')

build() {
  cd ..
  ./autogen.sh
  ./configure --prefix=/usr \
    --sysconfdir=/etc \
    --with-gnu-ld \
    --enable-gtk-doc

  #https://bugzilla.gnome.org/show_bug.cgi?id=656231
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool

  make
}

package() {
  cd ..
  make DESTDIR="$pkgdir" install

  # Temporary fix to FS#32361
  rm -rf "$pkgdir"/usr/include/libfm
  mv "$pkgdir"/usr/include/libfm-1.0/ "$pkgdir"/usr/include/libfm
}
