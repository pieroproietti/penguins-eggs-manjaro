# Maintainer: Stefano Capitani <stefano_at_manjaro_org>

pkgname=penguins-eggs
pkgver=9.0.5
pkgrel=1
_commit='e31644627f62a5e428e96df4cd0ecc498c685ee0'
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
sha256sums=('1c2b00929d59afd5f177a53e3e0be68f25c61cce3b42d8db0e0bd83fa6bffd4c')

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

