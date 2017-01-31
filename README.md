使用过其他一些 vim
配置，但实际上，如果不是自己配置的，很难能掌握各种插件的用法和各种快捷键操作。所以，干脆还是抽时间自己把需要的配置都简单的罗列出来，方便自己查找。

## 基本配置

### <leader> 键

<leader> 键，也就是前缀建，实际上，如果你觉得你的快捷键够用的话，这个是可以不需要的。为了方便，我将前缀建设置成了分号，这样，我们不用移动手指就能按到

```
" 定义快捷键的前缀<Leader>
let mapleader=";
```

### 文件类型侦测

包括编码检测，文件类型检测（使得对应的文件可以加载对应的插件和语法高亮等）等等

```
" 编码检测
set fileencodings=utf-8,gb2312,gb18030,gbk,ucs-bom,cp936,latin1
" 开启文件类型侦测
filetype on
" 根据侦测到的不同类型加载对应的插件
filetype plugin indent on
" 语法高亮、补全
syntax on
```

### 基本UI配置，包括高亮，缩进等

```
" color scheme
set background=dark
" color vividchalk
" 高亮当前行
au WinLeave * set nocursorline nocursorcolumn
au WinEnter * set cursorline cursorcolumn
set cursorline cursorcolumn
" 编辑器设定
set history=1000
set nocompatible
set nofoldenable                                                  " disable folding"
set confirm                                                       " prompt when existing from an unsaved file
set backspace=indent,eol,start                                    " More powerful backspacing
set t_Co=256                                                      " Explicitly tell vim that the terminal has 256 colors "
set mouse=a                                                       " use mouse in all modes
set report=0                                                      " always report number of lines changed                "
set wrap                                                          " dont wrap lines
set scrolloff=5                                                   " 5 lines above/below cursor when scrolling
set number                                                        " show line numbers
set showmatch                                                     " show matching bracket (briefly jump)
set showcmd                                                       " show typed command in status bar
set title                                                         " show file in titlebar
set laststatus=2                                                  " use 2 lines for the status bar
set matchtime=2                                                   " show matching bracket for 0.2 seconds
set matchpairs+=<:>                                               " specially for html
" set relativenumber
" 默认缩进
set autoindent
set smartindent     " indent when
set tabstop=4       " tab width
set softtabstop=4   " backspace
set shiftwidth=4    " indent width
set textwidth=80
set smarttab
set expandtab       " expand tab to space
" 特定文件缩进
autocmd FileType php,ruby,sass,scss,css,coffee,javascript setlocal tabstop=2 shiftwidth=2 softtabstop=2 textwidth=120
autocmd FileType python setlocal tabstop=4 shiftwidth=4 softtabstop=4 textwidth=120
autocmd FileType html,htmldjango,xhtml,haml setlocal tabstop=2 shiftwidth=2 softtabstop=2 textwidth=0
autocmd FileType elixir,ex,exs setlocal tabstop=2 shiftwidth=2 softtabstop=2 textwidth=120
" syntax support
autocmd Syntax javascript set syntax=jquery   " JQuery syntax support
" js
let g:html_indent_inctags = "html,body,head,tbody"
let g:html_indent_script1 = "inc"
let g:html_indent_style1 = "inc"
```

### 基本快捷键设置

```
" 定义快捷键到行首和行尾
nmap LB 0
nmap LE $
" 设置快捷键将选中文本块复制至系统剪贴板
vnoremap <Leader>y "+y
" 设置快捷键将系统剪贴板内容粘贴至 vim
nmap <Leader>p "+p
" 定义快捷键关闭当前分割窗口
nmap <Leader>q :q<CR>
" 定义快捷键保存当前窗口内容
nmap <Leader>w :w<CR>
" 定义快捷键保存所有窗口内容并退出 vim
nmap <Leader>WQ :wa<CR>:q<CR>
" 不做任何保存，直接退出 vim
nmap <Leader>Q :qa!<CR>
" 依次遍历子窗口
nnoremap nw <C-W><C-W>
" 定义快捷键在结对符之间跳转
nmap <Leader>M %
"
" 跳转至右方的窗口
" nnoremap <Leader>lw <C-W>l
" 跳转至左方的窗口
" nnoremap <Leader>hw <C-W>h
" 跳转至上方的子窗口
" nnoremap <Leader>kw <C-W>k
" 跳转至下方的子窗口
" nnoremap <Leader>jw <C-W>j
" 分割窗口之间跳转，跟上面冲突，自选一个
nnoremap <c-j> <c-w>j
nnoremap <c-k> <c-w>k
nnoremap <c-h> <c-w>h
nnoremap <c-l> <c-w>l
"
" When editing a file, always jump to the last cursor position
autocmd BufReadPost *
      \ if ! exists("g:leave_my_cursor_position_alone") |
      \     if line("'\"") > 0 && line ("'\"") <= line("$") |
      \         exe "normal g'\"" |
      \     endif |
      \ endif

" w!! to sudo & write a file
cmap w!! %!sudo tee >/dev/null %
" 快速重新加载 vimrc 文件
nmap <silent> <leader>ev :e $MYVIMRC<CR>
nmap <silent> <leader>sv :so $MYVIMRC<CR>
" for macvim(GUI)
" 只对 gvim 有效
if has("gui_running")
    set go=aAce  " remove toolbar
    "set transparency=30
    set guifont=Monaco:h13
    set showtabline=2
    set columns=140
    set lines=40
    noremap <D-M-Left> :tabprevious<cr>
    noremap <D-M-Right> :tabnext<cr>
    map <D-1> 1gt
    map <D-2> 2gt
    map <D-3> 3gt
    map <D-4> 4gt
    map <D-5> 5gt
    map <D-6> 6gt
    map <D-7> 7gt
    map <D-8> 8gt
    map <D-9> 9gt
    map <D-0> :tablast<CR>
endif
```

### 基本搜索

```
" 开启实时搜索功能
set incsearch
" 搜索时大小写不敏感
set ignorecase
" 关闭兼容模式
set nocompatible
" vim 自身命令行模式智能补全
set wildmenu
set smartcase
```

### 快速运行

```
map <F8> :call CompileRunGcc()<CR>
func! CompileRunGcc()
    exec "w"
    if &filetype == 'c'
        exec "!g++ % -o %<"
        exec "!time ./%<"
    elseif &filetype == 'cpp'
        exec "!g++ % -o %<"
        exec "!time ./%<"
    elseif &filetype == 'java'
        exec "!javac %"
        exec "!time java %<"
    elseif &filetype == 'sh'
        :!time bash %
    elseif &filetype == 'python'
        exec "!time python2.7 %"
    elseif &filetype == 'html'
        exec "!firefox % &"
    elseif &filetype == 'go'
        exec "!go build %<"
        exec "!time go run %"
    elseif &filetype == 'mkd'
        exec "!~/.vim/markdown.pl % > %.html &"
        exec "!firefox %.html &"
    endif
endfunc
```

## 插件管理
