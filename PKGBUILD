# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Massimiliano Torromeo <massimiliano.torromeo@gmail.com>
# Contributor: William J Bowman <bluephoenix47@gmail.com>

pkgbase=python-certifi
pkgname=('python-certifi' 'python2-certifi')
_libname=${pkgbase/python-/}
pkgver=2015.04.28
pkgrel=1
pkgdesc="Python package for providing Mozilla's CA Bundle"
arch=(any)
url="http://pypi.python.org/pypi/certifi"
license=('GPL')
makedepends=('python-setuptools' 'python2-setuptools')
source=("http://pypi.python.org/packages/source/${_libname:0:1}/$_libname/$_libname-$pkgver.tar.gz")
sha512sums=('c63287d9e0814226a1eb6ea0f6d1a53f0fd88995c0c2541e404efd0c70471fae01cb56ecca5425c6754342c28c96948ba912bd860bf2d336bba95a0b751f8f99')

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
