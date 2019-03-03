# vim-jetpack
A (very) minimal bash script to [g]et packages for Vim 8+ and Neovim, as a companion to the "packages" feature (see `:help packages` in Vim).

![vim-jetpack](https://caksoylar.github.io/vjp/vjp.png)

## Features
* Clone and update Vim plugins from remote git repos
* Display changelogs after updating
* Build tags for help files
* Parallel execution
* About 50 lines of pure bash, requiring `git` and coreutils components `mktemp`, `xargs`
  
## Non-features
* Removing unmanaged packages
* Cloning from non-master branches 

## Usage
Create a file (e.g. `plugins.txt`) specifying plugins to clone and where to put them, consisting of two columns separated with whitespace. Use `start` for regular packages and `opt` for packages to lazy load using `packadd`:
```bash
$ cat ~/.vim/plugins.txt
start https://github.com/tpope/vim-commentary
start https://github.com/tpope/vim-fugitive
start https://github.com/romainl/vim-cool
opt   https://github.com/mbbill/undotree
start https://caksoylar@dev.azure.com/caksoylar/caksoylar/_git/caksoylar
# comment lines are ignored
```

If it doesn't exist, create a directory to place remote plugins in Vim path:
```bash
$ mkdir -p ~/.vim/pack/remote
```

Call `vjp` with plugins file and packages folder as arguments:
```bash
$ vjp ~/.vim/plugins.txt ~/.vim/pack/remote 8
```
Last argument is optional and specifies the number of workers if you would like to run in parallel.
