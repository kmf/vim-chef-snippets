vim-chef-snippets
====================

This repository contains snippets files for Chef and InSpec for the [vim-snipmate](https://github.com/garbas/vim-snipmate.git) plugin for Vim.

How to install
-------------
Unfortunately there are many ways to how to install vim plugins. If you don't see your preferred way of installation plugins please consider updating this section. Basically, installation consists of 2 simple steps:

- Install [vim-snipmate](https://github.com/garbas/vim-snipmate)
- Install [vim-chef-snippets](https://github.com/kmf/vim-chef-snippets)

Using [Plug](https://github.com/junegunn/vim-plug)
-------------

add this to your `.vimrc`

```VimL
    " Install snipmate dependencies:    
    Plug 'MarcWeber/vim-addon-mw-utils'
    Plug 'tomtom/tlib_vim'
    " Install snipmate:
    Plug 'garbas/vim-snipmate'
    " Chef and InSpec Snippets for Vim
    Plug 'kmf/vim-chef-snippets'
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