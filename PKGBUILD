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
_commit=b286f6b3bd8fcb6439cea55083deadd59ae06f91
source=("git+https://github.com/crosstool-ng/crosstool-ng.git#commit=$_commit")
sha512sums=('2e1b815bc8b7e6ea3106ea98f1fc2f27fba84d87e58f567866f9c5f1c9cc69d2131b1b5ef74e92ec2745ac4f741f76931aba382dd4756657d1e47d91a369e2c4')
b2sums=('e62b966594b5643b4926d5b624b3d5e4c7bd7c3ce9dfe7a8793967ce84892b3447bb4933d9082a8ad0759b3d9f75a0e6210e2902304a1045f3811fda45ffc98f')

pkgver() {
  cd "$_pkgname"
  (
    set -o pipefail
    git describe --long --abbrev=7 2>/dev/null | sed $(printf 's/%s-//;s\([^-]*-g\)/r\1/;s/-/./g' "$_pkgname") ||
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
