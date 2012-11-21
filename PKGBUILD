# Maintainer: Massimiliano Torromeo <massimiliano.torromeo@gmail.com>
# Contributor: Patrice Peterson <runiq at archlinux dot us>
# Contributor: William J Bowman <bluephoenix47@gmail.com>

pkgname=python-certifi
_libname=${pkgname/python-/}
pkgver=0.0.8
pkgrel=1
pkgdesc="Mozilla's SSL Certs, Python 3 version"
arch=(any)
url="http://pypi.python.org/pypi/certifi"
license=('GPL')
depends=('python')
makedepends=('python-distribute')
source=(http://pypi.python.org/packages/source/${_libname:0:1}/$_libname/$_libname-$pkgver.tar.gz)

build() {
    cd "$srcdir/$_libname-$pkgver"
    python setup.py build
}

package() {
    cd "$srcdir/$_libname-$pkgver"
    python setup.py install --root="$pkgdir"
	install -m0644 -D "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

sha256sums=('46ecf5f7526a08cc1f8bc8232adf0cffce046f46ceff95539daec42ebc4849ef')
