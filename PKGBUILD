# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: David Runge <dvzrv@archlinux.org>
# Contributor: Massimiliano Torromeo <massimiliano.torromeo@gmail.com>
# Contributor: William J Bowman <bluephoenix47@gmail.com>

_py="python"
_pkg=certifi
pkgname="${_py}-${_pkg}"
pkgver=2024.07.04
pkgrel=1
pkgdesc="Python package for providing Mozilla's CA Bundle (using system CA store)"
arch=(
  any
)
_http="https://github.com"
url="${_http}/${_pkg}/${pkgname}"
license=(
  MPL-2.0
)
depends=(
  ca-certificates
  "${_py}"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-pytest"
)
source=(
  "${url}/archive/refs/tags/${pkgver}.tar.gz"
)
sha512sums=(
  '38e966f291b358a80ba862e3988da2fc1ab920f005abdfb0053b81b44aee827a657a4569b0c8fd76fd55235589eca21c01d7d36c4229ed3d0a7afdd51f3b92f8'
)
b2sums=(
  'a1323f1d69f05caebf492620c5cb27c3d272a92a061aacdc6a1fb894b301218eaf96f1768a8894b9b57bef0a99c3205a825e312db6fb8d2c0f6a217257a1afbe'
)

_get_usr() {
  local \
    _cc \
    _bin \
    _usr
  _cc="$( \
    command \
      -v \
      "cc")"
  _bin="$( \
    dirname \
      "${_cc}")"
  _usr="$( \
    dirname \
      "${_bin}")"
  echo \
    "${_usr}"
}

prepare() {
  cd \
    "${pkgname}-${pkgver}"
  # Use system CA store.
  # Replacing the copy in the source tree
  # so the test suite is actually run against it.
  ln \
    -sf \
    "$(_get_usr)/etc/ssl/certs/ca-certificates.crt" \
    certifi/cacert.pem
  # Our CA store has non-ASCII comments,
  # but we are not packaging for JVM
  # https://github.com/certifi/python-certifi/issues/50
  sed \
    -i \
    's/encoding="ascii"/encoding="utf-8"/' \
    certifi/core.py
}

build() {
  cd \
    "${pkgname}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${pkgname}-${pkgver}"
  pytest
}

package() {
  local \
    site_packages \
    python_version
  site_packages=$( \
    python \
      -c \
      "import site; print(site.getsitepackages()[0])")
  python_version=$( \
    "${_py}" \
      -c \
     'import sys; print(".".join(map(str, sys.version_info[:2])))'
  )
  cd \
    "${pkgname}-${pkgver}"
  "${_py}" \
    -m installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  # Replace CA store here again because
  # the symlink was installed as a file
  # install \
  #   -dm755 \
  #   "${pkgdir}/usr/lib/python${python_version}/site-packages/${_pkg}"
  ln \
    -sf "$(_get_usr)/etc/ssl/certs/ca-certificates.crt" \
    "${pkgdir}/usr/lib/python${python_version}/site-packages/${_pkg}/cacert.pem"
  install \
    -Dm644 LICENSE \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}
