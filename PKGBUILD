# Maintainer: Stefano Capitani <stefano_at_manjaro_org>

pkgname=penguins-eggs
pkgver=9.1.29
pkgrel=1
_commit='29f20ce50a8fcdb855a70a40603a7c8b40163421'
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
sha256sums=('991c68f7f934091ad32d3e107337dc65f0a3971639ccbae776bfdb4529e8dd02')

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

