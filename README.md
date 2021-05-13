### Look at these, rather use these methods it's more sustainable.

|![vim_vscode_chef_snippets](https://user-images.githubusercontent.com/78700/118138738-f6e5f080-b406-11eb-9c5d-a7e07ecbee52.gif)|![Cookstyle_linting_in_Vim](https://user-images.githubusercontent.com/78700/118148458-e0449700-b410-11eb-9817-cbfb9a90797c.gif)|
|-|-|
|[Confguring Vim to use VSCode Snippets for Chef](Confguring_Vim_to_use_VSCode_Snippets_for_Chef.md)|[Using Cookstyle in Vim, powered by ALE](Using_Cookstyle_in_Vim.md)|

-----

Rather not use vim-chef-snippets
====================

This repository contains snippets files for Chef and InSpec for the [vim-snipmate](https://github.com/garbas/vim-snipmate.git) plugin for Vim.


How to install
-------------
Unfortunately there are many ways to how to install vim plugins. If you don't see your preferred way of installation plugins please consider updating this section. Basically, installation consists of 2 simple steps:

- Install [vim-snipmate](https://github.com/garbas/vim-snipmate)
- Install [vim-chef-snippets](https://github.com/kmf/vim-chef-snippets)


Using [Plug](https://github.com/junegunn/vim-plug)
-------------

### Installation of Plug

[Download plug.vim](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim)
and put it in the "autoload" directory.

#### For Vim

###### Unix

```sh
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

You can automate the process by putting the command in your Vim configuration
file as suggested [here][auto].

[auto]: https://github.com/junegunn/vim-plug/wiki/tips#automatic-installation

###### Windows (PowerShell)

```powershell
iwr -useb https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim |`
    ni $HOME/vimfiles/autoload/plug.vim -Force
```

#### For Neovim

###### Unix, Linux

```sh
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```

###### Linux (Flatpak)

```sh
curl -fLo ~/.var/app/io.neovim.nvim/data/nvim/site/autoload/plug.vim \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

###### Windows (PowerShell)

```powershell
iwr -useb https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim |`
    ni "$(@($env:XDG_DATA_HOME, $env:LOCALAPPDATA)[$null -eq $env:XDG_DATA_HOME])/nvim-data/site/autoload/plug.vim" -Force
```
-------------
### Installation of the Vim Chef Snippets

add this to your `.vimrc`

```VimL
call plug#begin('~/.vim/plugged')
"
" Install snipmate dependencies:    
Plug 'MarcWeber/vim-addon-mw-utils'
Plug 'tomtom/tlib_vim'
" Install snipmate:
Plug 'garbas/vim-snipmate'
" Chef and InSpec Snippets for Vim
Plug 'kmf/vim-chef-snippets'
"
call plug#end()
```

just set your syntax to either, `chef` or `inspec`

In Vim for Chef:
```
set ft=chef
```

In Vim for InSpec:
```
set ft=inspec
```

Type a resource name and press `<TAB>`

Contribution
-------------

If you would like to contribute to this project, then just fork it in github and send a pull request. 

License
-------------

https://spdx.org/licenses/Apache-2.0.html

How is this built?
-------------

Mostly scraping Chef and InSpec docs.
It's ... bad ... 🤗 it will be ok.

For Chef:
```ruby
require 'yaml'

Dir.glob('*.yaml') do |doc|
  docs = YAML.load_file(doc)
  out =  docs.fetch("syntax_full_code_block")
  File.write(doc +".snip", out)
end
```

For InSpec: 
```ruby
Dir.glob('*.md').each do |doc|
  docs = File.read(doc)
  out =  docs.match(/(describe.*[\s\S]*?end)$/)[1]
  File.write(doc +".snip", out)
end
# Spacing to files
# sed -i -e 's/^/  /' *.snip
# Adding a newline to each file
# sed -i -e '$G' *.snip
```

Bye!
-------------
See you at ChefConf
