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
        "/templates",
        "/wardrobe.d"
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
