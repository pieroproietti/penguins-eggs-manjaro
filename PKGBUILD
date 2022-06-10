# Maintainer: Stefano Capitani <stefano_at_manjaro_org>


pkgname=penguins-eggs
pkgver=9.1.30
pkgrel=1
_commit='5fc4e767fb254755b84c35dd55dc62bf13553d67'
pkgdesc="A console utility that allows you to remaster your system and redistribute it as ISO images or via remote boot PXE."
arch=('x86_64')
url="https://penguins-eggs.net"
license=('GPL2')
# I see here something who bring 
depends=('arch-install-scripts' 'erofs-utils' 'manjaro-tools-iso' 'mtools' 'nodejs' 'python' 'syslinux' 'xdg-utils')
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

	# before, our mistake we copied all
	# now, just that we need specified in package.json
	# plus ./mkinitcpio for manjaro
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

	# Symlink man page
	install -d "${pkgdir}/usr/share/man/man1"
	ln -s "/usr/lib/${pkgname}/manpages/doc/man/eggs.roll.gz" "$pkgdir/usr/share/man/man1/eggs.1.gz"
}


