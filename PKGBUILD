# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Massimiliano Torromeo <massimiliano.torromeo@gmail.com>
# Contributor: William J Bowman <bluephoenix47@gmail.com>

pkgbase=python-certifi
pkgname=('python-certifi' 'python2-certifi')
_libname=${pkgbase/python-/}
pkgver=2015.9.6.1
pkgrel=1
pkgdesc="Python package for providing Mozilla's CA Bundle"
arch=(any)
url="http://pypi.python.org/pypi/certifi"
license=('GPL')
makedepends=('python-setuptools' 'python2-setuptools')
source=("http://pypi.python.org/packages/source/${_libname:0:1}/$_libname/$_libname-$pkgver.tar.gz")
sha512sums=('1b44a71c564da97c79bf76bd8e4b29b752fd5849bccb209b6e97a239370126acc2562937ed010135f2cc45cf78438cc4b113906dc7dc9b45507e9f33ac9f8988')

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
