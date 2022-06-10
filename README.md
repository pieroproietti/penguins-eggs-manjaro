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
        "/scripts",
        "/templates"
    ],
```

I'm not expert at all in manjaro, so I have a bit difficult to understand "the way", with time I hope to learn a bit.


# build and install penguins-eggs on manjaro OS

Create a directory to build penguins-eggs:
```
mkdir penguins-eggs
cd penguins-eggs
wget https://raw.githubusercontent.com/pieroproietti/penguins-eggs-manjaro/main/PKGBUILD
makepkg -si
```

Just download it from [penguins-eggs PKBUID](https://raw.githubusercontent.com/pieroproietti/penguins-eggs-manjaro/main/PKGBUILD) 


```makepkg -si```


# release
To create a new release, just edit followig lines in PKBUILD, essentiallt pkgver and _commit.

```
pkgver=9.1.29
pkgrel=1
_commit='29f20ce50a8fcdb855a70a40603a7c8b40163421'
```

# Dipendenze

Mi sembrano un po' troppe, in particolare snapd?

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
