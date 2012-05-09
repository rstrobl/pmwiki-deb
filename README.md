# Debian package for pmwiki

see http://www.pmwiki.org/ for upstream package

## Setting up the packaging environment

* install packaging tool suite:

	```
    aptitude install build-essential debhelper devscripts quilt
    ```
* create debian quilt alias in ~/.bashrc

	```
    alias dquilt="quilt --quiltrc=${HOME}/.quiltrc-dpkg"
   	```
* create ~/.quiltrc-dpkg

	```
    d=. ; while [ ! -d $d/debian -a `readlink -e $d` != / ]; do d=$d/..; done
    if [ -d $d/debian ] && [ -z $QUILT_PATCHES ]; then
        # if in Debian packaging tree with unset $QUILT_PATCHES
        QUILT_PATCHES="debian/patches"
        QUILT_PATCH_OPTS="--reject-format=unified"
        QUILT_DIFF_ARGS="-p ab --no-timestamps --no-index --color=auto"
        QUILT_REFRESH_ARGS="-p ab --no-timestamps --no-index"
        QUILT_COLORS="diff_hdr=1;32:diff_add=1;34:diff_rem=1;31:diff_hunk=1;33:diff_ctx=35:diff_cctx=33"
        if ! [ -d $d/debian/patches ]; then mkdir $d/debian/patches; fi
    fi
	```
    
## Updating upstream package

* clone this repository and run `uscan` from the root of it 
* extract the downloaded upstream package
* move the debian directory into it
* run `dch -v newversion-1`
* add entry: "New upstream release."
* apply patches by running: `while dquilt push; do dquilt refresh; done`
* make changes
* run `dpkg-buildpackage -uc -us`