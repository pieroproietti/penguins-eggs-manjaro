# penguins-eggs-manjaro

This is a fork of [penguins-eggs PKGBUILD](https://gitlab.manjaro.org/packages/community/penguins-eggs), created from the author 
to investigate about the problems of the package eggs on manjaro.

# build and install

```
pamac update
```
If your are with bash, I suggest to install bash-completion.

```
pamac install bash-completion
```

## Installing

### manjaro-tools-iso 

Copy and paste follow instructions:
```
git clone https://gitlab.manjaro.org/tools/development-tools/manjaro-tools
sudo cp manjaro-tools/initcpio/hooks/ /usr/lib/initcpio/ -R
sudo cp manjaro-tools/initcpio/install/ /usr/lib/initcpio/ -R
sudo cp manjaro-tools/initcpio/script/miso_shutdown /etc/initcpio/
```

### penguins-eggs

Copy and paste follow instructions:

```
mkdir try-penguins-eggs
cd try-penguins-eggs
wget https://raw.githubusercontent.com/pieroproietti/penguins-eggs-manjaro/main/PKGBUILD
wget https://raw.githubusercontent.com/pieroproietti/penguins-eggs-manjaro/main/penguins-eggs.install
makepkg -srcCi

```

# Hot to create a new release (memo for me)
To create a new release, just edit followig lines in PKBUILD, essentiallt pkgver and _commit.

```
pkgver=9.1.29
pkgrel=1
_commit='29f20ce50a8fcdb855a70a40603a7c8b40163421'
```
