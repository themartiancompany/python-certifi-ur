# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Massimiliano Torromeo <massimiliano.torromeo@gmail.com>
# Contributor: William J Bowman <bluephoenix47@gmail.com>

pkgbase=python-certifi
pkgname=('python-certifi' 'python2-certifi')
_libname=${pkgbase/python-/}
pkgver=2016.8.31
pkgrel=1
pkgdesc="Python package for providing Mozilla's CA Bundle"
arch=(any)
url="http://pypi.python.org/pypi/certifi"
license=('GPL')
makedepends=('python-setuptools' 'python2-setuptools')
source=("https://pypi.io/packages/source/${_libname:0:1}/$_libname/$_libname-$pkgver.tar.gz")
sha512sums=('2f54c1fec800ed37e750cbb2f75cd34e9593ee7c84ab77d7ce42424d940ed1a96be5dc90f37c0627683c00a2f92ef1bae4d4aa3628b3513a27f02a7459fb988c')

prepare() {
  cp -a $_libname-$pkgver{,-py2}

  cd $_libname-$pkgver-py2
  sed -i '1s|python$|python2|' certifi/core.py
}

build() {
  cd "$srcdir/$_libname-$pkgver"
  python setup.py build

  cd "$srcdir/$_libname-$pkgver-py2"
  python2 setup.py build
}

package_python-certifi() {
  depends=('python')

  cd "$srcdir/$_libname-$pkgver"
  python setup.py install --skip-build -O1 --root="$pkgdir"
  install -m0644 -D "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

package_python2-certifi() {
  depends=('python2')

  cd "$srcdir/$_libname-$pkgver-py2"
  python2 setup.py install --skip-build -O1 --root="$pkgdir"
  install -m0644 -D "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
