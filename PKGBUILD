# Maintainer: jay-tux <untoldjaydev [at] yandex 'period' com>
pkgname=jbuild
pkgver=0.1
pkgrel=1
epoch=
pkgdesc="A simple project generator for C/C++/CUDA written in zsh"
arch=('any')
url="https://github.com/jay-tux/jbuild"
license=('MPL2')
groups=()
depends=('zsh')
makedepends=()
checkdepends=()
optdepends=('git' 'curl' 'gcc' 'nvcc')
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=()
noextract=()
sha512sums=()
validpgpkeys=()

package() {
  install -dm755 "$pkgdir"/usr/bin/
  install -m755  "$srcdir"/jbuild "$pkgdir"/usr/bin
  install -m755  "$srcdir"/jbuild-help "$pkgdir"/usr/bin
}
