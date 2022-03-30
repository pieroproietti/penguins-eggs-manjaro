# Maintainer: Stefano Capitani <stefano_at_manjaro_org>

pkgname=penguins-eggs
pkgver=9.0.48
pkgrel=1
_commit='23ef6af7b0b2662bf6599c2f44c07c8603651a2e'
pkgdesc="A terminal utility, in active development, which allows you to remaster your system and redistribute it as an ISO image, on a USB stick or through the network via PXE remote boot"
arch=('x86_64')
url='https://penguins-eggs.net'
_url='https://github.com/pieroproietti/penguins-eggs'
license=('GPL2')
depends=('manjaro-tools-iso' 'nodejs' 'python' 'xdg-utils' 'arch-install-scripts' 'erofs-utils' 'mtools' 'syslinux' 'bash-completion')
makedepends=('npm')
conflicts=('penguins-eggs-dev')
replaces=('penguins-eggs-dev')
options=('!strip')
install=$pkgname.install
source=("$_url/archive/$_commit.tar.gz")
sha256sums=('15efdb4ecd66641db8017639cb91da5cb4a57b02a8f71b9582f1e8b7b1d17d25')

prepare() { 

	mv $pkgname-$_commit $pkgname

}

pkgver() {

    cd ${srcdir}/${pkgname}
	grep 'version' package.json | awk 'NR==1 {print $2 }' | awk -F '"' '{print $2}'
	
}

package() {

	# Copy executable to package directory
	mkdir -p "${pkgdir}/usr/lib/${pkgname}/"
	mkdir -p "${pkgdir}/usr/bin"

	# Install dependency modules
	cd $srcdir/$pkgname
	npm install tpc 
	npm run build
	

	# Copy the app files & dependency modules to package directory
	cp -r ./* "${pkgdir}/usr/lib/${pkgname}/"

	# Copy a license file to package directory
	mkdir -p "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	mv "${srcdir}/$pkgname/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE" 
	
	# Remove all md files
	rm -f "${pkgdir}/usr/lib/${pkgname}/*.md" 
	rm -Rf "${pkgdir}/usr/lib/${pkgname}/documents"
	
}

