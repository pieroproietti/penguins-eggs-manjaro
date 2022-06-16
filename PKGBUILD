# Maintainer: Stefano Capitani <stefano_at_manjaro_org>


pkgname=penguins-eggs
pkgver=9.1.31
pkgrel=1 
_commit='128acf836944ad8ee0e6ea2b3f0751edef213228' # mkinitcpio manjaro krill install


pkgdesc="Console utility to remaster and install your system."
arch=('x86_64')
url="https://penguins-eggs.net"
license=('GPL2')

# dependencies with manjaro-tools-iso, It work, but brings a lot of stuffs
# depends=('arch-install-scripts' 'erofs-utils' 'manjaro-tools-iso' 'mtools' 'nodejs' 'npm' 'python' 'syslinux' 'xdg-utils')

# cleaning dependencies, it work too, read README
depends=('arch-install-scripts' 'awk' 'dosfstools' 'e2fsprogs' 'erofs-utils' 'findutils' 'gzip' 'libarchive' 'libisoburn' 'lvm2' 'mtools' 'nodejs' 'openssl' 'pacman' 'parted' 'rsync' 'sed' 'syslinux' 'squashfs-tools')
makedepends=('git' 'pnpm')

# There is a way makepkg -si ask to install them? 
optdepends=('bash-completion' 'calamares' )
conflicts=('penguins-eggs-dev')
replaces=('penguins-eggs-dev')
options=('!strip')
source=("git+https://github.com/pieroproietti/penguins-eggs.git#commit=${_commit}")
sha256sums=('SKIP')

install=$pkgname.install

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
