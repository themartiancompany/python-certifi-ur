# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Massimiliano Torromeo <massimiliano.torromeo@gmail.com>
# Contributor: William J Bowman <bluephoenix47@gmail.com>

pkgbase=python-certifi
pkgname=('python-certifi' 'python2-certifi')
_libname=${pkgbase/python-/}
pkgver=2016.8.8
pkgrel=1
pkgdesc="Python package for providing Mozilla's CA Bundle"
arch=(any)
url="http://pypi.python.org/pypi/certifi"
license=('GPL')
makedepends=('python-setuptools' 'python2-setuptools')
source=("https://pypi.io/packages/source/${_libname:0:1}/$_libname/$_libname-$pkgver.tar.gz")
sha512sums=('adceffbe0875c90d4440ff193bbfee0da10d7dba23d323206cd3b2b14b9a1dad5886d243f23b8e5048b6062d142a872911475e7a0b043506e0f8f778777f325c')

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
