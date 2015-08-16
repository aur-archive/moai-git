# Maintainer: Federico Rampazzo < frampone at gmail >

pkgname=moai-git
pkgver=20130208
pkgrel=1
pkgdesc='An Open Source cross-platform LUA-based tool to develop games, focused on mobile'
arch=('i686' 'x86_64')
url='https://github.com/moai/moai-dev'
license=('custom:CPAL')
depends=('freeglut')
makedepends=('git')

source=('CPAL')
sha256sums=('30d53bf709e16d849116bff147c59e4dfc8091672c324fc6af9caac1881c80ac')

_gitroot='git://github.com/moai/moai-dev.git'
_gitname='moai-dev'

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
    cd "$_gitname" && git checkout linux
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"
  git submodule init
  git submodule update

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  chmod +x $srcdir/$_gitname-build/bin/build-linux.sh
  $srcdir/$_gitname-build/bin/build-linux.sh
}

package() {
  install -Dm755 "$srcdir/$_gitname-build/build/build-linux/moai" "$pkgdir/usr/bin/moai"
  install -Dm644 "$srcdir/CPAL" "$pkgdir/usr/share/licenses/$pkgname/CPAL"
}




