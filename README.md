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
## Build and install penguins-eggs

Copy and paste follow instructions
```
git clone https://github.com/pieroproietti/penguins-eggs-manjaro
cd penguins-eggs-manjaro
makepkg -srcCi
```
## Create your first iso, just CLI installer krill
```sudo eggs produce --fast```

## Create your first desktop iso, installer calamares
```sudo eggs calamares --install```
```sudo eggs produce --fast```

## Copy your iso image and boot the son of your system
You can use ventoy, simple USB, iso file with proxmox ve, virtualbox, vmware etc.


# Develop and collaborations link
* penguins-eggs discussion on [manjaro-forum](https://forum.manjaro.org/t/penguins-eggs-help-needed-for-manjaro-compatibility/96799)
* penguins-eggs PKGBUILD on [community](https://gitlab.manjaro.org/packages/community/penguins-eggs)
* penguins-eggs PKGBUILD [my way](https://github.com/pieroproietti/penguins-eggs-manjaro) (*)
* penguins-eggs [sources](https://github.com/pieroproietti/penguins-eggs)
* penguins-eggs [book](https://penguins-eggs.net/book/)
* penguins-eggs [blog](https://penguins-eggs.net)

(*) Here we refere always to that, but I hope with same help to solve the problems and have it in community again.


## Notes

### manjaro-tools-iso 

From manjaro-toos-iso really we need just this, it work the same:

Copy and paste follow instructions:
```
git clone https://gitlab.manjaro.org/tools/development-tools/manjaro-tools
sudo cp manjaro-tools/initcpio/hooks/ /usr/lib/initcpio/ -R
sudo cp manjaro-tools/initcpio/install/ /usr/lib/initcpio/ -R
sudo cp manjaro-tools/initcpio/script/miso_shutdown /etc/initcpio/
```


# How to create a new release (memo for me)
To create a new release, just edit followig lines in PKBUILD, essentiallt pkgver and _commit.

```
pkgver=9.1.29
pkgrel=1
_commit='29f20ce50a8fcdb855a70a40603a7c8b40163421'
```
