# Maintainer: Daniel Alejandro <dalejan051@gmail.com>


pkgname=simpmusic-bin
_pkgver=1.0.1-hf
pkgver=1.0.1_hf
appver=1.0.1
pkgrel=3
pkgdesc="A FOSS YouTube Music client for Android and Desktop with many features from
Spotify, SponsorBlock, ReturnYouTubeDislike using Compose Multiplatform to develop."
arch=(x86_64)
url="https://www.simpmusic.org"
license=("GPL-3.0")

depends=("gstreamer" "gst-plugins-good" "gst-plugins-bad" "yt-dlp")
conflicts=("${pkgname%}")
options=("!strip" "!debug")

# source=(
#   "https://github.com/maxrave-dev/SimpMusic/releases/download/v${_pkgver}/simpmusic_${appver}_amd64.deb"
# )
source=(
    "https://nightly.link/maxrave-dev/SimpMusic/workflows/desktop-deb-package/dev/desktop-deb-package.zip"
)
sha256sums=('SKIP')

prepare() {
    bsdunzip desktop-deb-package.zip
    bsdtar -xf "simpmusic_${appver}_amd64.deb"
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
