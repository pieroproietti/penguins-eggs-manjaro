# Maintainer: Stefano Capitani <stefano_at_manjaro_org> Piero Proietti <piero.proietti_at_gmail.com>
pkgname=penguins-eggs
pkgver=9.1.32 # autoupdate
pkgrel=1
# pkgdir
# pkgbase
pkgdesc="Console utility to remaster and reinstall your system."
arch=('any')
url="https://penguins-eggs.net"
license=('GPL2')
# groups=
depends=('arch-install-scripts' 'awk' 'dosfstools' 'e2fsprogs' 'erofs-utils' 'findutils' 
		 'glibc-locales' 'gzip' 'libarchive' 'libisoburn' 'lvm2' 'manjaro-tools-iso' 'mtools' 
		 'nodejs' 'openssl' 'pacman' 'parted' 'rsync' 'sed' 'syslinux' 'squashfs-tools')
optdepends=('bash-completion: type eggs commands more quickly'
			'calamares: system installer GUI' )
makedepends=('git' 'pnpm')
# checkdepends
# provides
# conflicts
# replaces
# backup
options=('!strip') # rimozioni varie, ma prende tempo...
install=$pkgname.install
_url_release="https://github.com/pieroproietti/penguins-eggs"
_branch_release="master"
_url_manjaro_tools="https://gitlab.manjaro.org/tools/development-tools/manjaro-tools"
source=("git+${_url_release}.git#branch=${_branch_release}")
#  we need too: "git+${_url_manjaro_tools}.git#branch=${_branch_release}"
changelog=changelog.md
# noextract
# md5sums
# sha1sums
sha256sums=('SKIP')



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
	install -Dm644 package.json -t "${pkgdir}/usr/lib/${pkgname}/"

	# We need them on /usr/lib/ not in /opt
	# I don't see problems. To change in /opt it's 
	# will be possible too, but need changes of sources
	cp -r ./addons "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./assets "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./bin "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./conf "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./lib "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./LICENSE "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./node_modules "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./mkinitcpio "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./pnpm-lock.yaml "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./README.md "${pkgdir}/usr/lib/${pkgname}/"
	cp -r ./scripts "${pkgdir}/usr/lib/${pkgname}/"

	# Symlink executable
	install -d "${pkgdir}/usr/bin"
	ln -s "/usr/lib/${pkgname}/bin/run" "${pkgdir}/usr/bin/eggs"

	# bash completions
	install -d "${pkgdir}/usr/share/bash-completion/completions"
	mv "${pkgdir}/usr/lib/${pkgname}/scripts/eggs.bash" "${pkgdir}/usr/share/bash-completion/completions/"

	# zsh completions
	install -d "${pkgdir}/usr/share/zsh/functions/Completion/Zsh/"
	mv "${pkgdir}/usr/lib/${pkgname}/scripts/_eggs" "${pkgdir}/usr/share/zsh/functions/Completion/Zsh/"

	# man page
	install -Dm644 manpages/doc/man/eggs.roll.gz "${pkgdir}/usr/share/man/man1/eggs.1.gz"

	# desktop link
	install -Dm644 "assets/${pkgname}.desktop" -t "${pkgdir}/usr/share/applications/"

	# icon
	install -Dm644 assets/eggs.png -t "${pkgdir}/usr/share/pixmaps/"
}
