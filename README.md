Its function is simple: _download, update and enable using `:packadd`_

It's limited only to GitHub repositories

Best utlized with, nomen omen, minimal list of plugins

## Installation

Execute in shell:

```sh
git clone https://github.com/Jorengarenar/minPlug.git ~/.vim/pack/plugins/opt/minPlug/
```

and in _vimrc_ add:

```vim
packadd minPlug " initialize minPlug
```

If you want to have _minPlug_ **automatically installed**, add this to your _vimrc_:

```vim
if empty(glob(substitute(&packpath, ",.*", "", "")."/pack/plugins/opt/minPlug")) " {{{
  call system("git clone --depth=1 https://github.com/Jorengarenar/minPlug ".
        \ substitute(&packpath, ",.*", "", "")."/pack/plugins/opt/minPlug")
  autocmd VimEnter * silent! MinPlugInstall | echo "minPlug: INSTALLED"
endif " }}}
```

## Usage

This plugin provides two commands: `MinPlug` and `MinPlugInstall`

### Add plugin

  After initialization of minPlug, use `MinPlug` in _vimrc_ in such fasion:

```vim
MinPlug username/repo branch
```

If `branch` isn't provided, as defualt `master` will be used

To disable plugin, simply comment out this line

Practiacal example: `MinPlug Jorengarenar/vim-darkness`

### On-demand loading

There is no on-demand loading in _minPlug_, but you can do:

```vim
MinPlug! username/repo branch
```

This will only add plugin to list, so you can download it, but it won't start automatically

Then you can use `autocmd` (or _ftplugin_) to load it on demand using `packadd`

Example:

```vim
MinPlug! Jorengarenar/fauxClip | autocmd filetype cpp packadd fauxClip
```

_**Please note, that this way is prone to bugs.**_

### Download/update plugins

```vim
:MinPlugInstall
```

When it finishes, only the message `DONE` will be shown

### Download/update plugins overriding local changes

```vim
:MinPlugInstall!
```

### Delete

Remove `MinPlug username/repo` line from _vimrc_, then go to `~/.vim/pack/plugins/opt` and remove the directory of plugin

---

#### Additional note

If you added something to the `packpath` option, ensure that your desired destination is first in the list (use `^=`, e.g. `set packpath^=$XDG_DATA_HOME/vim`)
