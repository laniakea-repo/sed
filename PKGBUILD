# Maintainer: Sébastien "Seblu" Luttringer <seblu@archlinux.org>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: judd <jvinet@zeroflux.org>

pkgname=sed
pkgver=4.9
pkgrel=1
pkgdesc='GNU stream editor'
arch=('x86_64')
url='https://www.gnu.org/software/sed/'
license=('GPL3')
groups=('base-devel')
depends=('glibc' 'acl' 'attr')
makedepends=('gettext')
source=("https://ftp.gnu.org/pub/gnu/sed/$pkgname-$pkgver.tar.xz"{,.sig})
validpgpkeys=('155D3FC500C834486D1EEA677FD9FCCB000BEEEE') #Jim Meyering <jim@meyering.net>
sha256sums=('6e226b732e1cd739464ad6862bd1a1aba42d7982922da7a53519631d24975181'
            'SKIP')

prepare() {
  cd $pkgname-$pkgver
  # apply patch from the source array (should be a pacman feature)
  local src
  for src in "${source[@]}"; do
    src="${src%%::*}"
    src="${src##*/}"
    [[ $src = *.patch ]] || continue
    msg2 "Applying patch $src..."
    patch -Np1 < "../$src"
  done
}

build() {
  cd $pkgname-$pkgver
  ./configure --prefix=/usr
  make
}

check() {
  cd $pkgname-$pkgver
  make check
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install
}

# vim:set ts=2 sw=2 et:
