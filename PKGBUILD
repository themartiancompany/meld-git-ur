# Maintainer: Jason Edson <jaysonedson@gmail.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>

_py='python'
_pkgname=meld
pkgname="${_pkgname}-git"
pkgver=3.21.3.6.g8112b4e8
pkgrel=2
pkgdesc='Visual diff and merge tool'
url="http://${_pkgname}merge.org"
license=(
  GPL)
arch=(
  any)
depends=(
  dconf
  glib2
  gsettings-desktop-schemas
  gtk3
  gtksourceview4
  "${_py}-cairo"
  "${_py}-gobject"
)
makedepends=(
  git
  meson
  yelp-tools
)
optdepends=(
  "${_py}-dbus: open a new tab in an already running instance")
provides=(
  "${_pkgname}=${pkgver}")
conflicts=(
  "${_pkgname}"
  "${_pkgname}-dev"
)
options=(
  !emptydirs)
_http="https://gitlab.gnome.org"
_ns="GNOME"
_url="${_http}/${_ns}/${_pkgname}"
source=(
  "git+${_url}.git")
sha256sums=(
  SKIP)

pkgver() {
  cd \
    "${_pkgname}"
  git \
    describe \
    --always | \
    sed \
      's|-|.|g'
}

_usr="$( \
  dirname \
   "$(gcc \
        -v 2>&1 |
        grep \
          "InstalledDir" | \
          awk '{print $2}')")"

_cflags=(
  "$( \
    [[ "${_usr}" != "" ]] && \
      echo "-I${_usr}/include/gtk-3.0")"
  "${CFLAGS}"
)

export \
  PKG

build() {
  CFLAGS="${_cflags[*]}" \
  CXXFLAGS="${_cflags[*]}" \
    arch-meson \
      build "${_pkgname}"
  CFLAGS="${_cflags[*]}" \
  CXXFLAGS="${_cflags[*]}" \
    meson \
      compile \
      -C build
}

package() {
  meson \
    install \
    -C build \
    --destdir "${pkgdir}"
}

# vim:set sw=2 sts=-1 et:
