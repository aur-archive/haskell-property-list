# Maintainer: Arch Haskell Team <arch-haskell@haskell.org>
_hkgname=property-list
pkgname=haskell-property-list
pkgver=0.0.1.0
pkgrel=4
pkgdesc="XML property list parser"
url="http://hackage.haskell.org/package/${_hkgname}"
license=('custom:PublicDomain')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' 'haskell-haxml>=1.19' 'haskell-bytestring=0.9.1.7' 'haskell-bytestring-class' 'haskell-category-extras' 'haskell-containers=0.3.0.0' 'haskell-dataenc' 'haskell-mtl' 'haskell-old-locale=1.0.0.2' 'haskell-pretty=1.0.1.1' 'haskell-syb=0.1.0.2' 'haskell-template-haskell=2.4.0.1' 'haskell-th-fold' 'haskell-time=1.1.4')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
}
md5sums=('27aa4e7d92845cee6fe062cd693479b6')
