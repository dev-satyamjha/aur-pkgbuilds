# Maintainer: Daniel Alejandro <dalejan051@gmail.com>


pkgname=simpmusic-bin
_pkgver=1.0.1-hf-1
pkgver=1.0.1_hf
appver=1.0.1
pkgrel=0
pkgdesc="A FOSS YouTube Music client for Android and Desktop with many features from
Spotify, SponsorBlock, ReturnYouTubeDislike using Compose Multiplatform to develop."
arch=(x86_64)
url="https://www.simpmusic.org"
license=("GPL-3.0")

depends=("gstreamer" "gst-plugins-good" "gst-plugins-bad" "yt-dlp")
conflicts=("${pkgname%}")
options=("!strip" "!debug")

source=(
  "https://github.com/maxrave-dev/SimpMusic/releases/download/v${_pkgver}/simpmusic_${appver}_amd64.deb"
)
sha256sums=('5e08b82b8e9303fafb638b952bd4357ea1b57288b02218052f7b0fe31309ed5f')

prepare() {
    bsdtar -xf data.tar.zst

    _basepath="${srcdir}/opt/simpmusic"
    # Add icon entry to .desktop
    grep -qfx "StartupWMClass=com-maxrave-simpmusic-MainKt" "${_basepath}/lib/simpmusic-SimpMusic.desktop" || \
    echo "StartupWMClass=com-maxrave-simpmusic-MainKt" >> "${_basepath}/lib/simpmusic-SimpMusic.desktop"
}

package() {
    # Install app
    cp -r --preserve=mode,timestamps opt/ "${pkgdir}/"

    _basepath="${pkgdir}/opt/simpmusic"

    # Install the icon
    if [[ -f "${srcdir}/opt/simpmusic/lib/SimpMusic.png" ]]; then
        install -Dm644 "${srcdir}/opt/simpmusic/lib/SimpMusic.png" \
            "${pkgdir}/usr/share/pixmaps/SimpMusic.png"
    fi

    # Install .desktop
    install -Dm644 "${_basepath}/lib/simpmusic-SimpMusic.desktop" \
        "${pkgdir}/usr/share/applications/simpmusic.desktop"

    # Permissions
    chmod 755 "${_basepath}/bin/SimpMusic" 2>/dev/null || true
}
