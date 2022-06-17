# Maintainer: Stefano Capitani <stefano_at_manjaro_org> Piero Proietti <piero.proietti_at_gmail.com>
pkgname=penguins-eggs
pkgver=9.1.31 # si autoaggiorna
pkgrel=1
_BRANCH=master
pkgdesc="Console utility remaster and reinstall your system."
arch=('any')
url='https://github.com/pieroproietti/penguins-eggs'
license=('GPL2')
depends=('arch-install-scripts' 'awk' 'dosfstools' 'e2fsprogs' 'erofs-utils' 'findutils' 
		 'gzip' 'libarchive' 'libisoburn' 'lvm2' 'mtools' 'nodejs' 'openssl' 'pacman' 
		 'parted' 'rsync' 'sed' 'syslinux' 'squashfs-tools')
makedepends=('git' 'pnpm')
optdepends=('bash-completion: eggs completition'
			'calamares: GUI installer' )
source=("git+${url}.git#branch=${_BRANCH}")
sha256sums=('SKIP')
install=$pkgname.install
options=('!strip') # rimozioni varie, ma prende tempo...

# pkgver
pkgver() {
	cd ${srcdir}/${pkgname}
	grep 'version' package.json | awk 'NR==1 {print $2 }' | awk -F '"' '{print $2}'
}

# build 
build() {
	cd ${srcdir}/${pkgname}
	pnpm i
	pnpm run build
}

# package
package() {
	install -d "${pkgdir}/usr/lib/${pkgname}"

	cd ${srcdir}/${pkgname}
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
