# Maintainer: Filippov Aleksey <sarum9in@gmail.com>
pkgname='bunsan.pm-git'
pkgver=20120613
pkgrel=1
pkgdesc="bunsan pm"
arch=('i686' 'x86_64')
url="https://github.com/sarum9in/bunsan_pm"
license=('GPL')
groups=()
depends=('bunsan.common-git' 'bunsan.utility-git' 'crypto++')
makedepends=('git' 'cmake')
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
source=()
noextract=()
md5sums=()

_gitroot="git://github.com/sarum9in/bunsan_pm.git"
_gitname="pm"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  mkdir build && cd build
  cmake .. -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release
  make $MAKEFLAGS
}

check() {
  cd "$srcdir/$_gitname-build/build"
  make test
}

package() {
  cd "$srcdir/$_gitname-build/build"
  make DESTDIR="$pkgdir/" install
}
