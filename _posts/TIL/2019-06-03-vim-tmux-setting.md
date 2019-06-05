---
layout: post
title: 잘 쓰는 vim, tmux 환경 
categories: TIL
---

최근에 Ubuntu를 쓰는 일이 잦아지면서 vim을 잘 쓰게 되었는데, setting하는 과정을 기억 못해서 글로 남긴다. 

###  ~/.vimrc
```
# CTAGS
set tags=/PATH-TO-CTAGS/tags
set nu

# CSCOPE
set csprg=/usr/bin/cscope

set csto=0
set cst
set nocsverb

function! AddCscopeDatabase()
let currentdir = getcwd()

while !filereadable("cscope.out") && getcwd() != "/"

cd ..
endwhile

if filereadable("cscope.out")
csc add cscope.out
endif

endfunction

call AddCscopeDatabase()
set csverb

```

### ~/.tmux.conf
```
set -g mouse on

setw -g mode-keys vi

# Use Alt-arrow keys without prefix key to switch panes
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# Shift arrow to switch windows
bind -n S-Left  previous-window
bind -n S-Right next-window

# scrollback buffer size increase
set -g history-limit 100000

# change window order
bind-key -n C-S-Left swap-window -t -1
bind-key -n C-S-Right swap-window -t +1

# disable window name auto change
set-option -g allow-rename off

# bar color
set -g status-bg black
set -g status-fg white

# toggle pane title visibility
bind T run 'zsh -c "arr=( off top ) && tmux setw pane-border-status \${arr[\$(( \${arr[(I)#{pane-border-status}]} % 2 + 1 ))]}"'
# rename pane
bind t command-prompt -p "(rename-pane)" -I "#T" "select-pane -T '%%'"
```
