# Maintainer: Jeremy MountainJohnson <jskier[at]gmail[dot]com>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Massimiliano Torromeo <massimiliano.torromeo@gmail.com>
# Contributor: Spider.007 <archlinux AT spider007 DOT net>

_pkgname=kibana
pkgname=kibana5
pkgver=5.6.10
pkgrel=1
pkgdesc='Browser based analytics and search dashboard for Elasticsearch5 series'
url='https://www.elastic.co/products/kibana'
arch=('any')
license=('Apache')
depends=('nodejs')
optdepends=('elasticsearch5')
provides=("kibana=$pkgver")
backup=('etc/kibana5/kibana.yml')
options=('!strip' 'emptydirs')
source=(https://artifacts.elastic.co/downloads/${_pkgname}/${_pkgname}-${pkgver}-linux-x86_64.tar.gz
        kibana5.service
        tmpfile.conf
        user.conf)
sha512sums=('c56c600c79bf2f5d2991d6c1442db300c78dd4135bf8dec5b9f500d609e2f041d09649195cfdae2f6d30cf8de2c2c865ac607283f865c4aa8ec1d400af84c270'
            '9a492283caf9389c9529707f0a44db6266ac097f624965b8b121dc538711cbf735c99841858738f3871feb4529b773d238c6c590d408153da36b9f164e3ef98c'
            '9d9208f3e5f78b07b7848c12c6d37d90a3eb0016545bb1f834ed6b4f605c11dffdf6fc2b33e00bf5fd6e5cb6164236b4f90042a7727abce619140ffab593c0d2'
            '58f2cb4c3dfd55b6467a9b66c26bfb31b28b2ee25fbf30c114befffd288203e8992a2661faf47869a0a97cd451060da790f5972033b90189ea52530e855e9f15')

prepare() {
  cd ${_pkgname}-${pkgver}-linux-x86_64
  # set default quiet mode for systemd, cli option forces specified values
  sed -r 's|#(logging.quiet:) false|\1 true|' -i config/kibana.yml
}

package() {
  cd ${_pkgname}-${pkgver}-linux-x86_64

  install -dm 755 "${pkgdir}/usr/share/kibana5"
  cp -a * "${pkgdir}/usr/share/kibana5"

  install -dm 750 "${pkgdir}/etc/kibana5"
  install -Dm 640 config/kibana.yml -t "${pkgdir}/etc/kibana5"
  install -Dm 644 "${srcdir}/kibana5.service" -t "${pkgdir}/usr/lib/systemd/system"
  install -Dm 644 "${srcdir}/user.conf" "${pkgdir}/usr/lib/sysusers.d/kibana5.conf"
  install -Dm 644 "${srcdir}/tmpfile.conf" "${pkgdir}/usr/lib/tmpfiles.d/kibana5.conf"

  rm -r "${pkgdir}/usr/share/kibana5/node"
}
