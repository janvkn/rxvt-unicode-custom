# Maintainer: Jan Van der Veken <janvkn[at]gmail[dot]com>
# Contributor: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Sébastien Luttringer
# Contributor: Angel Velasquez <angvp@archlinux.org>
# Contributor: tobias <tobias@archlinux.org>
# Contributor: dibblethewrecker dibblethewrecker.at.jiwe.dot.org

pkgbase=rxvt-unicode-custom
pkgname=('rxvt-unicode-custom' 'rxvt-unicode-custom-terminfo')
pkgver=9.30
pkgrel=4
arch=('x86_64')
url='http://software.schmorp.de/pkg/rxvt-unicode.html'
license=('GPL')
makedepends=('libxft' 'libxt' 'perl' 'startup-notification' 'libnsl')
source=(http://dist.schmorp.de/rxvt-unicode/rxvt-unicode-${pkgver}.tar.bz2
        urxvt.desktop
        urxvtc.desktop
        urxvt-tabbed.desktop
        font-width-fix.patch
        line-spacing-fix.patch
        no-confirm-paste.patch)
sha256sums=('fe1c93d12f385876457a989fc3ae05c0915d2692efc59289d0f70fabe5b44d2d'
            '5f9c435d559371216d1c5b49c6ec44bfdb786b12d925d543c286b0764dea0319'
            '91536bb27c6504d6cb0d33775a0c4709a4b439670b900f0c278c25037f19ad66'
            'ccd7c436e959bdc9ab4f15801a67c695b382565b31d8c352254362e67412afcb'
            '686770fe4e8d6bb0ba497ad2e1f217d17515f2544d80abe76496c63ead2bfaa4'
            '546a388d0595404a59c71c3eaeba331031032a75f96c57e9a860f27bbd7ebfcc'
            '759f534864a47aaac4fddd5960c8d161636d192a2e1db23a93dc8a69d85a7030')
sha512sums=('048d5f635a61bc1a739d5cbc09e7a9f77cee18c81df468ce1ff0a62866ced06fc4ec258bb015d2484a7e7bad2339f0bdd79bd824d649c2553a80bdef9f199e99'
            '7184714a908071a4e8e5c065c5f90255e94dfd072df459c8d6f66fca3647781b3d1f6908b9303bcfd0d5b3f2e3822a8d66efaaa8a7c4d44f6e682839031a6e99'
            'aa501eeeb220ba03b3f101b160230612efbca87694fef88c469b2976d29769c24b34576ea82f6c7941fad6039ac776f32e397add9b957b49bf2e84aeb67b66d6'
            '18c7afb0c3eb8c832893b9ead09d25374b70ae1cd5479a5291d11794906c53daa6f1a1bf698b37efda062bb2b991cacac53a0a6c185ca416b8718fde2bb6a7af'
            '77fb097c7fd9f4a49372728002bd73c9eed602ee55906926c11d2a39c08114715df18dc4c0b7e78ba1a2755f207a681a95a2cba1bb5d49d7891fc3b7a5870f05'
            '579114c37e7734ad5ae6567e012856a2d8baef355c9762126ab1b081babede8e923740e4f2b34068767b1b49baa3f191e35cdb9e1601805ba10b830fa0cda6d5'
            'b211a31615ece3c8496524d5ea7e05d749a9bd7c5d5762bfdfbb69c28d9f2569cd58c93a2dd47c8aaf76bcfb8a41457ec0b3cee4aee1e3fd5fc4b2e24bece67d')

prepare() {
  cd rxvt-unicode-${pkgver}
  patch -p0 -i ../font-width-fix.patch
  patch -p0 -i ../line-spacing-fix.patch
  patch -p0 -i ../no-confirm-paste.patch
  rm -f src/perl/confirm-paste
}
build() {
  cd rxvt-unicode-${pkgver}
  # we disable smart-resize (FS#34807)
  # do not specify --with-terminfo (FS#46424)
  ./configure \
    --prefix=/usr \
    --enable-256-color \
    --enable-combining \
    --enable-fading \
    --enable-font-styles \
    --enable-iso14755 \
    --enable-keepscrolling \
    --enable-lastlog \
    --enable-mousewheel \
    --enable-next-scroll \
    --enable-perl \
    --enable-pointer-blank \
    --enable-rxvt-scroll \
    --enable-selectionscrolling \
    --enable-slipwheeling \
    --enable-smart-resize \
    --enable-startup-notification \
    --enable-transparency \
    --enable-unicode3 \
    --enable-utmp \
    --enable-wtmp \
    --enable-xft \
    --enable-xim \
    --enable-xterm-scroll 
  make
}

package_rxvt-unicode-custom() {
  pkgdesc='Unicode enabled rxvt-clone terminal emulator (urxvt)'
  depends=('rxvt-unicode-custom-terminfo' 'libxft' 'perl' 'startup-notification' 'libnsl' 'libptytty')
  optdepends=('gtk2-perl: to use the urxvt-tabbed')
  conflicts=('rxvt-unicode')
  provides=('rxvt-unicode')

  # install freedesktop menu
  for _f in urxvt urxvtc urxvt-tabbed; do
    install -Dm 644 ${_f}.desktop "${pkgdir}/usr/share/applications/${_f}.desktop"
  done

  cd rxvt-unicode-${pkgver}
  # workaround terminfo installation
  export TERMINFO="${srcdir}/terminfo"
  install -d "${TERMINFO}"
  make DESTDIR="${pkgdir}" install
  # install the tabbing wrapper ( requires gtk2-perl! )
  sed -i 's/\"rxvt\"/"urxvt"/' doc/rxvt-tabbed
  install -Dm 755 doc/rxvt-tabbed "${pkgdir}/usr/bin/urxvt-tabbed"
}

package_rxvt-unicode-custom-terminfo() {
  pkgdesc='Terminfo files for urxvt'
  conflicts=('rxvt-unicode<=9.18-6' 'rxvt-unicode-terminfo')
  provides=('rxvt-unicode-terminfo')
  install -dm 755 "${pkgdir}/usr/share/"
  mv terminfo "${pkgdir}/usr/share/"
}

# vim: ts=2 sw=2 et:
