# Maintainer: Connor Prussin <connor at prussin dot net>

# If you find problems with the package, create an issue on Github:
# https://github.com/cprussin/avpnc

pkgname=avpnc-fips
pkgver=1.5
pkgrel=1
pkgdesc="Aviatrix VPN Client. Helps connect to VPN Networks. Supports SAML and password based authentication"
arch=('any')
url='http://docs.aviatrix.com/Downloads/samlclient.html'
license=('custom')
depends=('gedit>=2.0.0' 'openvpn>=2.3.0' 'zlib' 'openresolv')
makedepends=('imagemagick')
options=(!strip emptydirs)
source=(https://aviatrix-download.s3-us-west-2.amazonaws.com/AviatrixVPNClient/dev/fips/AVPNC_debian_FIPS.deb
        logrotate
        service
        browser
        AVPNC.desktop)
sha512sums=('369f008fdeff19c299b61d5d06557a038ae7ffd564955731295942dacb9bebaeeef725f9eeb280ae5f584e5ca9e0e2b7d8f9b317f4db6e8ee9c18a52d4fe8ca9'
            '4a64702faa88eda3150d8ad144a2359e55914f8041545ef0335990de5f546ae9b9eac00d56ebc8b4937077ad6d3694f66ce9c16014cc2f89b3a2dc599172569a'
            '0a3ba4025967160cea890864b8e89c2b547806220ea704c4bfaff6459dc7d87a3008d5b928f48e7da8a32821400725a0338d8dea3ee823c913a540018bdc35ce'
            '0e9d281face2c0730d61978e633e06fec453a7d7b217410db4b0fd3cbec2544e644353b6d6394eca5426c14e77e917dbdc4426b31460783f121ceba3acb41f5b'
            '380b42872ea6ece12f17bc7e175417fcea2e4d4ac063cac38d857c2f80cfef90d3e5efae0fc8826e9914ff35c23f9e8873826d7998b3a95d84d0f48a67948b5d')

package() {
  bsdtar -xf ${srcdir}/data.tar.xz -C ${srcdir}/

  # Install files to their correct locations (avpnc upstream has a really
  # nonstandard structure)
  install -Dm755 ${srcdir}/usr/bin/AVPNC_bin/AVPNC \
          ${pkgdir}/usr/bin/AVPNC_bin/AVPNC
  install -Dm755 ${srcdir}/usr/bin/AVPNC_bin/AVPNC_RP \
          ${pkgdir}/usr/bin/AVPNC_bin/AVPNC_RP
  install -Dm644 ${srcdir}/usr/bin/AVPNC_bin/libcrypto.so \
          ${pkgdir}/usr/bin/AVPNC_bin/libcrypto.so
  install -Dm644 ${srcdir}/usr/bin/AVPNC_bin/libcrypto.so.1.0.0 \
          ${pkgdir}/usr/bin/AVPNC_bin/libcrypto.so.1.0.0
  install -Dm644 ${srcdir}/usr/bin/AVPNC_bin/libssl.so \
          ${pkgdir}/usr/bin/AVPNC_bin/libssl.so
  install -Dm644 ${srcdir}/usr/bin/AVPNC_bin/libssl.so.1.0.0 \
          ${pkgdir}/usr/bin/AVPNC_bin/libssl.so.1.0.0
  install -Dm755 ${srcdir}/usr/bin/AVPNC_bin/openvpn \
          ${pkgdir}/usr/bin/AVPNC_bin/openvpn
  install -Dm755 ${srcdir}/usr/bin/AVPNC_bin/scripts/linux.sh \
          ${pkgdir}/usr/bin/AVPNC_bin/scripts/linux.sh
  install -Dm644 ${srcdir}/usr/share/doc/avpnc/copyright \
          ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE

  # Convert icon to correct size and install into correct location
  mkdir -p ${pkgdir}/usr/share/icons/hicolor/128x128/apps
  chmod 755 ${pkgdir}/usr/share/icons/hicolor/128x128/apps
  convert -resize 128x128 ${srcdir}/usr/bin/AVPNC_bin/Avi.png \
          ${pkgdir}/usr/share/icons/hicolor/128x128/apps/${pkgname}.png

  # Install log directory
  mkdir -p ${pkgdir}/var/log/${pkgname}
  chmod 755 ${pkgdir}/var/log/${pkgname}

  # Install local scripts
  install -Dm644 ../logrotate ${pkgdir}/etc/logrotate.d/${pkgname}
  install -Dm644 ../service ${pkgdir}/usr/lib/systemd/system/${pkgname}.service
  install -Dm755 ../browser ${pkgdir}/usr/bin/AVPNC_bin/browser
  install -Dm644 ../AVPNC.desktop ${pkgdir}/usr/share/applications/${pkgname}.desktop
}
