# Maintainer: Mark Wagie <mark at manjaro dot org>
# Contributor: Christian Rebischke <chris.rebischke@archlinux.org>
# Contributor: Jeff Henson <jeff@henson.io>
# Contributor: Ron Asimi <ron dot asimi at gmail dot com>
# Contributor: Roman Perepelitsa <roman.perepelitsa@gmail.com>

pkgname=zsh-theme-powerlevel10k
pkgver=1.20.0
pkgrel=3
 pkgdesc="Powerlevel10k is a theme for Zsh. It emphasizes speed, flexibility and out-of-the-box experience."
 arch=('x86_64')
 url='https://github.com/romkatv/powerlevel10k'
 license=('MIT')
depends=('glibc' 'zsh' 'gitstatus')
 optdepends=(
   'ttf-meslo-nerd-font-powerlevel10k: recommended font'
   'powerline-fonts: patched fonts for powerline')
 replaces=('zsh-theme-powerlevel9k')
 source=("powerlevel10k-${pkgver}.tar.gz::https://github.com/romkatv/powerlevel10k/archive/v${pkgver}.tar.gz")
sha256sums=('d8187d44b697b3a37a8c4896678b4380e717cbf2850179529358348780a2d3d7')

 package() {
  cd "powerlevel10k-${pkgver}"
  # only copy over the files we need
  install -D LICENSE "${pkgdir}/usr/share/license/${pkgname}"
  install -d "${pkgdir}/usr/share/${pkgname}"
  install powerlevel10k.zsh-theme powerlevel9k.zsh-theme \
    prompt_powerlevel10k_setup prompt_powerlevel9k_setup \
    "${pkgdir}/usr/share/${pkgname}"

  find config internal -type f -exec install -D '{}' "${pkgdir}/usr/share/${pkgname}/{}" ';'
  # p10k expects gistatus to be under the p10k directory, so create a symlink
  ln -s /usr/share/gitstatus "${pkgdir}/usr/share/${pkgname}/gitstatus"

   cd "${pkgdir}/usr/share/${pkgname}"
  for file in *.zsh-theme internal/*.zsh; do
     zsh -fc "emulate zsh -o no_aliases && zcompile -R -- $file.zwc $file"
   done
 }
