# Maintainer: Stefano Capitani <stefano_at_manjaro_org>

pkgname=penguins-eggs
pkgver=9.1.29
pkgrel=1
_commit='29f20ce50a8fcdb855a70a40603a7c8b40163421'
pkgdesc="A console utility that allows you to remaster your system and redistribute it as ISO images or via remote boot PXE."
arch=('x86_64')
url="https://penguins-eggs.net"
license=('GPL2')
depends=('manjaro-tools-iso' 'nodejs' 'python' 'xdg-utils' 'arch-install-scripts' 'erofs-utils' 'mtools' 'syslinux')
makedepends=('git' 'pnpm')
optdepends=('bash-completion')
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
	cp -r ./* "${pkgdir}/usr/lib/${pkgname}/"

	# Symlink executable
	install -d "${pkgdir}/usr/bin"
	ln -s "/usr/lib/${pkgname}/bin/run" "${pkgdir}/usr/bin/eggs"

	# Symlink bash completions
	install -d "${pkgdir}/usr/share/bash-completion/completions"
	ln -s /usr/lib/${pkgname}/scripts/eggs.bash "${pkgdir}/usr/share/bash-completion/completions/"

	# Symlink man page
	install -d "${pkgdir}/usr/share/man/man1"
	ln -s "/usr/lib/${pkgname}/manpages/doc/man/eggs.roll.gz" "$pkgdir/usr/share/man/man1/eggs.1.gz"
}

