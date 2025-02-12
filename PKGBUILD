# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.


# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Chih-Hsuan Yen <yan12125@archlinux.org>
# Contributor: Kyle Keen <keenerd@gmail.com>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_proj="jaraco"
_component="collections"
_pkg="${_proj}.${_component}"
pkgname="${_py}-${_pkg}"
pkgver=5.1.0
pkgrel=1
_pkgdesc=(
  "Models and classes to supplement"
  "the stdlib 'collections' module."
)
arch=(
  'any'
)
_http="https://github.com"
_ns="${_proj}"
url="${_http}/${_ns}/${_pkg}"
license=(
  'MIT'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-${_proj}.text"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools-scm"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-pytest"
)
conflicts=(
  "${_py}-jaraco"
)
replaces=(
  "${_py}-jaraco"
)
source=(
  "${_pkg}-${pkgver}.tar.gz::${url}/archive/refs/tags/v${pkgver}.tar.gz"
)
sha512sums=(
  '6dfb5bf22e55a5148e8c846bf2d3f5a6c628bbe2034b8425153c3978aeff738a9fe00e426e7e2c421827e8a87e5270716d211d9ee42eed786d81e14791cec842'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  SETUPTOOLS_SCM_PRETEND_VERSION="${pkgver}" \
  "${_py}" \
    -m \
      build \
      --wheel \
      --no-isolation
}

check() {
  local \
    pytest_options=()
  pytest_options=(
    -vv
  )
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      pytest \
      "${pytest_options[@]}"
}

package() {
  local \
    site_packages
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
      --destdir="${pkgdir}" \
      "dist/"*".whl"
  # Symlink license file
  site_packages="$( \
    "${_py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")"
  install \
    -d \
      "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${site_packages}/${_pkg}-${pkgver}.dist-info/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim:set ts=2 sw=2 et:
