# Maintainer: Bernd Amend <berndamend gmail com>

_gitname=k8055
pkgname=${_gitname}-git
pkgver=d787c88
pkgrel=2
pkgdesc="git version of k8055"
arch=('i686' 'x86_64')
url="https://github.com/jeremyz/k8055"
license=('LGPL')
conflicts=('libk8055')
provides=('libk8055')
source=("git+https://github.com/jeremyz/${_gitname}.git")
md5sums=('SKIP')
depends=('libusbx' 'wxgtk')

pkgver() {
	cd $_gitname
	# Use the tag of the last commit
	git describe --always | sed 's|-|.|g'
}

build() {
	cd $_gitname
	sed -i "s/prefix=@CMAKE_INSTALL_PREFIX@/prefix=\/usr/g" libk8055/k8055.pc.in
	sed -i "s/prefix=@CMAKE_INSTALL_PREFIX@/prefix=\/usr/g" libk8055/k8055++.pc.in
	sed -i "s/GROUP=\"k8055\"/GROUP=\"users\"/g" velleman.rules
	mkdir build
	cd build
	cmake -DCMAKE_INSTALL_PREFIX="$pkgdir/usr" ..
	make
}

package() {
	cd $_gitname/build
	make install
	mkdir -p "$pkgdir/usr/share/man"
	mv "$pkgdir/usr/man" "$pkgdir/usr/share/man"
	install -Dm644 ../velleman.rules "$pkgdir/etc/udev/rules.d/70-velleman.rules"
}
