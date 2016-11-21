# Config

## bashrc

```bash
PS1='\[\e[0;34m\]\u\[\e[m\]:\[\e[1;34m\]\w\[\e[m\]$(__git_ps1 "\[\e[3;36m\](%s)")\[\e[0;0m\]\$ '
PS2='> '
PS3='> '
PS5='+ '

HISTSIZE=1000
HISTFILESIZE=2000
tac ~/.bash_history | awk '!x[$0]++' | tac | sponge ~/.bash_history

bind '"\e[A": history-search-backward'
bind '"\e[B": history-search-forward'
```

## inputrc

```bash
set show-all-if-unmodified on
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

set clipboard=unnamed
```
