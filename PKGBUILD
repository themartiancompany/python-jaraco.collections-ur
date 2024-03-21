# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Chih-Hsuan Yen <yan12125@archlinux.org>
# Contributor: Kyle Keen <keenerd@gmail.com>

pkgname=python-jaraco.collections
_name="${pkgname#python-}"
pkgver=3.5.2
pkgrel=3
pkgdesc="Models and classes to supplement the stdlib 'collections' module."
arch=('any')
url='https://github.com/jaraco/jaraco.collections'
license=('MIT')
depends=('python-jaraco.text' 'python-jaraco.classes')
makedepends=('python-build' 'python-installer' 'python-setuptools-scm' 'python-wheel')
checkdepends=('python-pytest-enabler' 'python-pytest-mypy')
conflicts=('python-jaraco')
replaces=('python-jaraco')
source=("$_name-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha512sums=('f112abd208627d7ea1ced21e2c76d09fd395b9d93019e940b008be3b3712d4add26ff3df6fd42acb87903f05d50051320bc812f0333f0a9ade8a6db029d5f25f')

prepare() {
  cd $_name-$pkgver
  # https://github.com/jaraco/jaraco.collections/issues/10
  echo "explicit_package_bases = True" >> mypy.ini
}

build() {
  cd $_name-$pkgver
  SETUPTOOLS_SCM_PRETEND_VERSION=$pkgver python -m build --wheel --no-isolation
}

check() {
  local pytest_options=(
    -vv
    --deselect docs/conf.py::mypy-status
    --deselect jaraco/collections.py::mypy
  )

  cd $_name-$pkgver
  python -m pytest "${pytest_options[@]}"
}

package() {
  cd $_name-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -Dm644 LICENSE -t "$pkgdir"/usr/share/licenses/$pkgname/
}

# vim:set ts=2 sw=2 et:
