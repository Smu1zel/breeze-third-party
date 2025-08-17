# Written by: Gustavo Alvarez <sl1pkn07@gmail.com>
# Contributor: FadeMind <fademind@gmail.com>
# Forked by: Smu1zel <lyndenl25@yahoo.com>

pkgname=breeze-third-party-git
pkgver=6.5
pkgrel=1
pkgdesc='Breeze icon theme for KDE Plasma (with third-party icons).'
arch=('any')
url='https://github.com/Smu1zel/breeze-third-party.git'
license=('LGPL')
groups=('kf6')
makedepends=(
  'extra-cmake-modules-git'
  'cmake'
  'git'
  'qt6-tools'
  'python'
  'python-lxml'
)
checkdepends=('fdupes')
provides=('breeze-icons')
conflicts=('breeze-icons')
source=('git+https://github.com/Smu1zel/breeze-third-party.git')
sha256sums=('SKIP')

pkgver(){
  cd breeze-third-party
  _ver="$(cat CMakeLists.txt | grep -m1 'KF_VERSION' | grep -o "[[:digit:]]*" | paste -sd'.')"
  echo "${_ver}.r$(git rev-list --count HEAD).$(git rev-parse --short HEAD)"
}

build() {
  cmake -S breeze-icons -B build \
    -DCMAKE_BUILD_TYPE=None \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DKDE_INSTALL_CMAKEPACKAGEDIR=/usr/share/cmake \
    -DBUILD_TESTING=ON \
    -DBINARY_ICONS_RESOURCE=ON

  cmake --build build
}

check() {
  cd build
  ctest --output-on-failure
}

package() {
  DESTDIR="${pkgdir}" cmake --install build
}
