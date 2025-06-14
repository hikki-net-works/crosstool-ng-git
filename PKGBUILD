# Maintainer: Ian P Bradley <crabapp@hikki.tech>

_pkgname=crosstool-ng
pkgname=$_pkgname-git
pkgver=crosstool.ng.1.27.0.r65.g93d5d76
pkgrel=1
pkgdesc="A versatile (cross-)toolchain generator."
arch=(x86_64 x86_64_v3 armv7h aarch64)
url="https://crosstool-ng.github.io"
license=('GPL')
depends=(ncurses make rsync)
makedepends=('git' 'flex' 'bison' 'gperf' 'help2man' 'unzip' 'lzip' 'python')
provides=($_pkgname)
_commit=93d5d7664faaf3a0e63c58cd74105c3c8364130b
source=("git+https://github.com/crosstool-ng/crosstool-ng.git#commit=$_commit")
sha512sums=('b72f8f31c12c9a6e13240ea3d4844dba752d9d9fccac8d22ea0d033288037949566c5a9f5fb66bff344b7fdb61d3fa839e5453ba3a4d534af081bfaa7dd8109e')
b2sums=('6c62fe08f1e07b8fc4a5b5e2812e5610c53e302b3c2677d9019f7f73ef89c1e90c32c6cbe16b3c55d6524f15f26dfa6de9e7bad17bd83be7e64d2d9d6b93c1f9')

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
