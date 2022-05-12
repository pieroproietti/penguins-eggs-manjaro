# Maintainer: Stefano Capitani <stefano_at_manjaro_org>

pkgname=penguins-eggs
pkgver=9.1.14
pkgrel=1
_commit='8f89c9ce5660f218e47203c8409ccfb7b37f6aca'
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
sha256sums=('82d3352030bf488c74a3c850044d8c3d8f03cac9a2306a66bbbcac4e0e92c64b')

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

