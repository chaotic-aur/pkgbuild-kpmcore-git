# Maintainer: Antonio Rojas <arojas@archlinux.org>

pkgname=kpmcore-git
pkgver=20.12.2
pkgrel=1
pkgdesc="Library for managing partitions"
arch=(x86_64)
url="https://www.kde.org/applications/system/kdepartitionmanager/"
license=(GPL2)
depends=(smartmontools kcoreaddons-git kwidgetsaddons-git ki18n-git polkit-qt5 qca-qt5-git)
makedepends=(extra-cmake-modules-git git)
conflicts=(${pkgname%-git})
provides=(${pkgname%-git})
optdepends=('e2fsprogs: ext2/3/4 support'
	    'xfsprogs: XFS support'
	    'jfsutils: JFS support'
	    'reiserfsprogs: Reiser support'
	    'ntfs-3g: NTFS support'
            'dosfstools: FAT32 support'
            'fatresize: FAT resize support'
            'f2fs-tools: F2FS support'
            'exfat-utils: exFAT support'
            'nilfs-utils: nilfs support'
            'udftools: UDF support')
source=('git+https://invent.kde.org/system/kpmcore.git')
sha256sums=('SKIP')

pkgver() {
  cd kpmcore
  _ver="$(cat CMakeLists.txt | grep -m3 -e MAJOR -e MINOR -e RELEASE | grep -o "[[:digit:]]*" | paste -sd'.')"
  echo "${_ver}.r$(git rev-list --count HEAD).$(git rev-parse --short HEAD)"
}

build() {
  cmake -B build -S kpmcore \
    -DCMAKE_INSTALL_LIBEXECDIR=lib \
    -DBUILD_TESTING=OFF
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
