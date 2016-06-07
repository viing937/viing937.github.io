# Config

## bashrc

```bash
HISTSIZE=1000
HISTFILESIZE=2000
tac ~/.bash_history | awk '!x[$0]++' | tac | sponge ~/.bash_history

bind '"\e[A": history-search-backward'
bind '"\e[B": history-search-forward'
```

## vimrc

```bash
syntax on
filetype plugin on

set number

set expandtab
set tabstop=4
set shiftwidth=4

set nobackup
set nowritebackup
set noswapfile
```
