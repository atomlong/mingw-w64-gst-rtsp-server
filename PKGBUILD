# Maintainer: drakkan <nicola.murino at gmail dot com>
pkgname=mingw-w64-gst-rtsp-server
pkgver=1.20.2
pkgrel=1
pkgdesc="RTSP server library based on GStreamer (mingw-w64)"
arch=(any)
url="http://gstreamer.freedesktop.org/"
license=('LGPL')
depends=('mingw-w64-gst-plugins-base')
options=('!strip' '!buildflags' 'staticlibs')
makedepends=('mingw-w64-meson')

source=("${url}src/gst-rtsp-server/gst-rtsp-server-${pkgver}.tar.xz")
sha256sums=('6a8e9d136bbee4fc03858a0680dd5cbf91e2e989c43da115858eb21fb1adbcab')

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
  cd "${srcdir}/gst-rtsp-server-${pkgver}"
  for _arch in $_architectures; do
    mkdir -p "build-${_arch}" && pushd build-${_arch}
    ${_arch}-meson \
      -D package-name="GStreamer (Arch Linux)" \
      -D package-origin="http://www.archlinux.org/" ..
    ninja
    popd
  done
}

package() {
  cd "${srcdir}/gst-rtsp-server-${pkgver}"
  for _arch in ${_architectures}; do
    DESTDIR="${pkgdir}" ninja -C "${srcdir}/gst-rtsp-server-${pkgver}/build-${_arch}" install
  done
}

# vim: ts=2 sw=2 et:
