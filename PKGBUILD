# Maintainer: My name <myemail at domain dot me>

_pkgname=visionaire-studio

pkgname="${_pkgname}"-appimage
pkgver=0.0.1
pkgrel=1
pkgdesc="Development for P&C games"
arch=('x86_64')
url="https://www.visionaire-studio.net/"
license=('custom:Unlicense')
makedepends=('7zip')
depends=('zlib' 'fuse2')
options=(!strip)
_appimage="Visionaire-Studio-Full-x86_64.AppImage"
source_x86_64=("${_appimage}")
noextract=("${_appimage}")
sha256sums_x86_64=('SKIP')

prepare() {
    chmod +x "${_appimage}"
    7z e -aoa "${_appimage}" -o./ visionaire-studio.desktop viseditor.svg BSD_3_Clause.txt LGPL2_1.txt libpng-LICENSE.txt MIT.txt webm.txt ZLIB.txt
    echo StartupWMClass=viseditor >> "${_pkgname}.desktop"
}

build() {
    # Adjust .desktop so it will work outside of AppImage container
    sed -i -E "s|Exec=./AppRun.sh|Exec=env DESKTOPINTEGRATION=false ${_pkgname}|" \
        "${_pkgname}.desktop"
}


package() {
    # AppImage
    install -Dm755 "${srcdir}/${_appimage}" "${pkgdir}/opt/${pkgname}/${pkgname}.AppImage"
    install -dm755 "${pkgdir}/opt/${pkgname}/Licenses/"

    install -Dm644 "${srcdir}/BSD_3_Clause.txt" "${pkgdir}/opt/${pkgname}/Licenses/BSD_3_Clause.txt"
    install -Dm644 "${srcdir}/LGPL2_1.txt" "${pkgdir}/opt/${pkgname}/Licenses/LGPL2_1.txt"
    install -Dm644 "${srcdir}/libpng-LICENSE.txt" "${pkgdir}/opt/${pkgname}/Licenses/libpng-LICENSE.txt"
    install -Dm644 "${srcdir}/MIT.txt" "${pkgdir}/opt/${pkgname}/Licenses/MIT.txt"
    install -Dm644 "${srcdir}/webm.txt" "${pkgdir}/opt/${pkgname}/Licenses/webm.txt"
    #install -Dm644 "${srcdir}/LICENSE" "${pkgdir}/opt/${pkgname}/Licenses/LICENSE"
    install -Dm644 "${srcdir}/ZLIB.txt" "${pkgdir}/opt/${pkgname}/Licenses/ZLIB.txt"

    # Desktop file
    install -Dm644 "${srcdir}/${_pkgname}.desktop" \
            "${pkgdir}/usr/share/applications/${pkgname}.desktop"

    # Icon images
    install -dm755 "${pkgdir}/usr/share/icons/hicolor/scalable/apps/"
    cp "${srcdir}/viseditor.svg" "${pkgdir}/usr/share/icons/hicolor/scalable/apps/"

    # Symlink executable
    install -dm755 "${pkgdir}/usr/bin"
    ln -s "/opt/${pkgname}/${pkgname}.AppImage" "${pkgdir}/usr/bin/${_pkgname}"

    # Symlink license
    install -dm755 "${pkgdir}/usr/share/licenses/${pkgname}/"

    ln -s "/opt/$pkgname/Licenses/BSD_3_Clause.txt" "$pkgdir/usr/share/licenses/$pkgname"
    ln -s "/opt/$pkgname/Licenses/LGPL2_1.txt" "$pkgdir/usr/share/licenses/$pkgname"
    ln -s "/opt/$pkgname/Licenses/libpng-LICENSE.txt" "$pkgdir/usr/share/licenses/$pkgname"
    ln -s "/opt/$pkgname/Licenses/MIT.txt" "$pkgdir/usr/share/licenses/$pkgname"
    ln -s "/opt/$pkgname/Licenses/webm.txt" "$pkgdir/usr/share/licenses/$pkgname"
    ln -s "/opt/$pkgname/Licenses/ZLIB.txt" "$pkgdir/usr/share/licenses/$pkgname"
}



#StartupWMClass=viseditor
