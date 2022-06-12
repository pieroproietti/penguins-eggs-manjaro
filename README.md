# penguins-eggs-manjaro

This is a fork of [penguins-eggs PKGBUILD](https://gitlab.manjaro.org/packages/community/penguins-eggs), created from the author 
to investigate about the problems of the package eggs on manjaro.

# build and install

```
pamac update
```
If your are with bash, I succest to install bash-completion, really usefull with CLI tools like eggs.

```
pamac install bash-completion
```

## Installing

### manjaro-tools-iso 

To not depend from manjaro-tools-iso, who bring a lot of stuffs not necessary for eggs, we need:

* copy [initcpio stuffs](https://gitlab.manjaro.org/tools/development-tools/manjaro-tools/-/tree/master/initcpio/hooks) from [manjaro-tools](https://gitlab.manjaro.org/tools/development-tools/manjaro-tools) to /usr/lib/initcpio/hooks
* copy manjaro-tools/initcpio/script/miso_shutdown in /etc/initcpio/ 

We don't need all manjaro-tools-iso stuffs, just the necessary to build .

Copy and paste follow instructions:
```
git clone https://gitlab.manjaro.org/tools/development-tools/manjaro-tools
sudo cp manjaro-tools/initcpio/hooks/ /usr/lib/initcpio/ -R
sudo cp manjaro-tools/initcpio/install/ /usr/lib/initcpio/ -R
sudo cp manjaro-tools/initcpio/script/miso_shutdown /etc/initcpio/
```

necessary files are:


* hooks/miso
* hooks/miso_pxe_common
* hooks/miso_pxe_nbd
* hooks/miso_shutdown
* hooks/miso_loop_mnt
* hooks/miso_pxe_http
* hooks/miso_pxe_nf

* install/miso
* installmiso_loop_mnt
* install/ miso_pxe_http
* install/miso_pxe_nfs
* install/miso_kms
* install/miso_pxe_common
* install/miso_pxe_nbd
* install/miso_shutdown

* script/miso_shutdown

### penguins-eggs

Copy and paste follow instructions:

```
mkdir try-penguins-eggs
cd try-penguins-eggs
wget https://raw.githubusercontent.com/pieroproietti/penguins-eggs-manjaro/main/PKGBUILD
makepkg -srcCi

```

# Dependencies problem includind manjaro-tools-iso in dependencies

I'm getting a lot of dependencies, particulary surprised from snapd, and at the moment I don't understand why.


* apparmor-3.0.4-1
* calamares-tools-0.1.0-1
* libburn-1.5.4-1
* libisoburn-1.5.4-2 *
* libisofs-1.5.4-1  libuv-1.43.0-1
* manjaro-iso-profiles-base-17.1.12-1
* manjaro-tools-base-git-r2996.d3ab091-1
* manjaro-tools-yaml-git-r2996.d3ab091-1
* mktorrent-1.1-4
* ruby-3.0.4-1
* ruby-irb-1.4.1-1
* ruby-kwalify-0.7.2-3
* ruby-reline-0.3.1-1
* rubygems-3.3.8-1
* snapd-2.55.5-1 
* arch-install-scripts-24-2  
* erofs-utils-1.4-2
* manjaro-tools-iso-git-r2996.d3ab091-1
* mtools-1:4.0.39-1
* nodejs-18.2.0-1
* syslinux-6.04.pre2.r11.gbf6db5b4-3

To analyze depends, we can use:
```
pacman -Sii manjaro-tools-iso-git | grep 'Depends On'
```
or:
```
pactree manjaro-tools-iso-git
```


# Hot to create a new release (memo for me)
To create a new release, just edit followig lines in PKBUILD, essentiallt pkgver and _commit.

```
pkgver=9.1.29
pkgrel=1
_commit='29f20ce50a8fcdb855a70a40603a7c8b40163421'
```
