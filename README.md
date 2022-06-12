# penguins-eggs-manjaro

This is a fork of [penguins-eggs PKGBUILD](https://gitlab.manjaro.org/packages/community/penguins-eggs), created from the author 
to investigate about the problems of the package eggs on manjaro.

Before - my mistake - we copy the entire sources on /usr/lib/penguins-eggs, when we need to copy just files specified
in package.json:

```
...

 "files": [
        "/assets",
        "/addons",
        "/bin",
        "/conf",
        "/lib",
        "/manpages",
        "/oclif.manifest.json",
        "/scripts"
    ],
```

I'm not expert at all in manjaro, so I have a bit difficult to understand "the way", with time I hope to learn a bit.


# build and install (users)

Copy and paste follow instructions:

```
mkdir try-penguins-eggs
cd try-penguins-eggs
wget https://raw.githubusercontent.com/pieroproietti/penguins-eggs-manjaro/main/PKGBUILD
makepkg -si

```

Usando ```makepkg -srcCi ``` ti installa quello che manca per fare il pacchetto, rimuove tutte le dipendenze usate solo per la costruzione e pulisce la cache del pacchetto ..



Or: create a directory - for example ```try-penguins-eggs``` - and just download the PKGBUILD from [penguins-eggs PKBUID](https://raw.githubusercontent.com/pieroproietti/penguins-eggs-manjaro/main/PKGBUILD) with your browser. After that ```cd  try-penguins-eggs```, finally: ```makepkg -si```


# New release (memo for me)
To create a new release, just edit followig lines in PKBUILD, essentiallt pkgver and _commit.

```
pkgver=9.1.29
pkgrel=1
_commit='29f20ce50a8fcdb855a70a40603a7c8b40163421'
```

# Dependencies problem

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

# analyze depends
use:
```
pacman -Sii manjaro-tools-iso-git | grep 'Depends On'
```
or:
```
pactree manjaro-tools-iso-git
```

# From manjaro-toos-iso we need just miso

```
==> ERROR: Hook 'miso_shutdown' cannot be found
==> ERROR: Hook 'miso' cannot be found
==> ERROR: Hook 'miso_loop_mnt' cannot be found
==> ERROR: Hook 'miso_kms' cannot be found
```

## how find them?

Of course whe can fing on [manjaro-tools](https://gitlab.manjaro.org/tools/development-tools/manjaro-tools), they live in /usr/lib/inipcpio

wget https://gitlab.manjaro.org/tools/development-tools/manjaro-tools/-/raw/master/initcpio/hooks/miso 
wget https://gitlab.manjaro.org/tools/development-tools/manjaro-tools/-/raw/master/initcpio/hooks/miso_shutdown
wget https://gitlab.manjaro.org/tools/development-tools/manjaro-tools/-/raw/master/initcpio/hooks/miso_loop_mnt
#wget https://gitlab.manjaro.org/tools/development-tools/manjaro-tools/-/raw/master/initcpio/hooks/miso_kms
mv miso* /usr/lib/initcpio/hooks



