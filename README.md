# penguins-eggs-manjaro

This is a fork of [penguins-eggs](https://gitlab.manjaro.org/packages/community/penguins-eggs), created from the author of penguins-eggs
to investigate about the problems of eggs manjaro package.

I'm not expert at all in manjaro, so I have a bit difficult to understand "the way", with time I hope to learn a bit.


# make and install
Just:

```makepkg -si```


# release
To create a new release, just edit followig lines in PKBUILD, essentiallt pkgver and _commit.

```
pkgver=9.1.29
pkgrel=1
_commit='29f20ce50a8fcdb855a70a40603a7c8b40163421'
```
