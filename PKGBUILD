# Maintainer: Ian P Bradley <crabapp@hikki.tech>

_pkgname=crosstool-ng
pkgname=$_pkgname-git
pkgver=crosstool.ng.1.27.0.r63.g0f69d3c
pkgrel=1
pkgdesc="A versatile (cross-)toolchain generator."
arch=(x86_64 x86_64_v3 armv7h aarch64)
url="https://crosstool-ng.github.io"
license=('GPL')
depends=(ncurses make rsync)
makedepends=('git' 'flex' 'bison' 'gperf' 'help2man' 'unzip' 'lzip' 'python')
provides=($_pkgname)
_commit=0f69d3cbeba1a913819445f2e1d57f36067f194b
source=("git+https://github.com/crosstool-ng/crosstool-ng.git#commit=$_commit")
sha512sums=('SKIP')
b2sums=('6fa71b517d77ec85dc98347a2bbcfae97febdb9179e442d116293532bc3bca8c974d3144d264fc942510362b1c5c751771eca5589dd7cf495f512ffa4121882a')

pkgver() {
  cd "$_pkgname"
  (
    set -o pipefail
    git describe --long --abbrev=7 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
      printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
  )
}

prepare() {
  cd "$_pkgname"
  ./bootstrap
}

build() {
  cd "$_pkgname"

  ./configure --prefix=/usr \
    --libexecdir=/usr/lib \
    --with-bash-completion \
    --with-ncurses

  make
}

check() {
  cd "$_pkgname"
  make -k check
}

package() {
  cd "$_pkgname"
  make DESTDIR="$pkgdir/" install
}
