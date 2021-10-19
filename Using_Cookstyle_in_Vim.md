# Configuring VIM to use Cookstyle for better Chef Cookbook Development, powered by ALE
![Cookstyle_linting_in_Vim](https://user-images.githubusercontent.com/78700/118148458-e0449700-b410-11eb-9817-cbfb9a90797c.gif)


Add this to your `.vimrc`
```
call plug#begin('~/.vim/plugged')

Plug 'dense-analysis/ale'
" Airline Optional
Plug 'vim-airline/vim-airline'

call plug#end()
```

```
" Ale begin
let g:ale_enabled = 1
"let g:ale_set_quickfix = 1
let g:ale_open_list = 1
let g:ale_sign_error = '❌'
let g:ale_sign_warning = '⚠️'
let g:ale_sign_info = '💡'
let g:ale_list_window_size = 8
let g:ale_ruby_rubocop_executable = '/opt/chef-workstation/bin/cookstyle'

autocmd FileType qf setlocal wrap

nmap <F8> :ALEFix rubocop<cr>
let g:ale_linters = {
      \   'ruby': ['rubocop']
      \}

" Airline + ALE
let g:airline#extensions#ale#enabled = 1
let g:ale_echo_msg_format = '[%linter%] %s [%severity%]'

" Ale end
```

Press `F8` to autocorrect
