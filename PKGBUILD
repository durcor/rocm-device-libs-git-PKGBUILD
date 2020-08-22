# Maintainer Tyler Kaminski <durcor at disroot dot org>
#
# Based on rocm-device-libs PKGBUILD maintained 
# by Ranieri Althoff <ranisalt+aur at gmail dot com>

pkgname=rocm-device-libs-git
_pkgname="${pkgname%-git}"
pkgver=r636.41b390c
pkgrel=1
pkgdesc='Radeon Open Compute - device libs'
arch=('x86_64')
url='https://github.com/RadeonOpenCompute/ROCm-Device-Libs'
license=('custom:NCSAOSL')
makedepends=(cmake llvm-amdgpu)
provides=("$_pkgname")
conflicts=("$_pkgname")
source=("$pkgname::git+$url")
sha256sums=('SKIP')

pkgver() {
  cd "$pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
    CC=/opt/rocm/llvm/bin/clang \
    cmake   -DCMAKE_INSTALL_PREFIX=/opt/rocm \
            -DLLVM_DIR=/opt/rocm/llvm/lib/cmake/llvm \
            "$pkgname"
    make
}

package() {
    DESTDIR="$pkgdir" make install
    install -Dm644 "$pkgname/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
