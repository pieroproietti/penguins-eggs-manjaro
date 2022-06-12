# Maintainer: Stefano Capitani <stefano_at_manjaro_org>


pkgname=penguins-eggs
pkgver=9.1.30
pkgrel=1
#_commit='1a821b62f5e4968fb8da8d13fe100426df1ef27c' # working old calamares definition
_commit='adb85ffab7e1eff1744083713916daf5f00228a6'

pkgdesc="Console utility to remaster your system and redsistribute it and more."
arch=('x86_64')
url="https://penguins-eggs.net"
license=('GPL2')
# I see here something who bring 
# depends=('arch-install-scripts' 'erofs-utils' 'manjaro-tools-iso' 'mtools' 'nodejs' 'npm' 'python' 'syslinux' 'xdg-utils')
depends=('arch-install-scripts' 'erofs-utils' 'libisoburn' 'mtools' 'nodejs' 'npm' 'python' 'syslinux' 'xdg-utils')
makedepends=('git' 'pnpm')

# There is a way makepkg -si ask to install them? 
optdepends=('bash-completion' 'calamares' )
conflicts=('penguins-eggs-dev')
replaces=('penguins-eggs-dev')
options=('!strip')
source=("git+https://github.com/pieroproietti/penguins-eggs.git#commit=${_commit}")
sha256sums=('SKIP')

pkgver() {
	cd ${srcdir}/${pkgname}
	grep 'version' package.json | awk 'NR==1 {print $2 }' | awk -F '"' '{print $2}'
}

build() {
	cd ${srcdir}/${pkgname}

	# Install dependency modules
	pnpm i
	pnpm run build
}

package() {
	cd ${srcdir}/${pkgname}

	# Copy the app files & dependency modules to package directory
	install -d "${pkgdir}/usr/lib/${pkgname}"

	# NOTE: pnpm i "${pkgname}" -g
	# this command will do the same, but will use;
	# /usr/lib/node_modules/penguins-eggs/

	# before we copy all, now just that is 
	# defined in files: [] on package.json
	cp -r ./addons "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./assets "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./bin "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./conf "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./lib "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./LICENSE "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./manpages "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./mkinitcpio "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./node_modules "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./package.json "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./pnpm-lock.yaml "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./README.md "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./scripts "${pkgdir}/usr/lib/${pkgname}/"

	# Symlink executable
	install -d "${pkgdir}/usr/bin"
	ln -s "/usr/lib/${pkgname}/bin/run" "${pkgdir}/usr/bin/eggs"

	# Symlink bash completions
	install -d "${pkgdir}/usr/share/bash-completion/completions"
	ln -s /usr/lib/${pkgname}/scripts/eggs.bash "${pkgdir}/usr/share/bash-completion/completions/"

	# Symlink zsh completions
	install -d "${pkgdir}/usr/share/zsh/functions/Completion/Zsh/"
	ln -s /usr/lib/${pkgname}/scripts/_eggs "${pkgdir}/usr/share/zsh/functions/Completion/Zsh/"

	# Symlink man page
	install -d "${pkgdir}/usr/share/man/man1"
	ln -s "/usr/lib/${pkgname}/manpages/doc/man/eggs.roll.gz" "$pkgdir/usr/share/man/man1/eggs.1.gz"
}


