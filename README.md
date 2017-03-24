# Atom-Bash-Profile


[[ -s "$HOME/.profile" ]] && source "$HOME/.profile" # Load the default .profile

[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM into a shell session *as a function*

#!/bin/bash

source ~/.git-completion.bash
source ~/.git-prompt.sh

MAGENTA="\[\033[0;35m\]"
YELLOW="\[\033[0;33m\]"
BLUE="\[\033[34m\]"
LIGHT_GRAY="\[\033[0;37m\]"
CYAN="\[\033[0;36m\]"
GREEN="\[\033[0;32m\]"

function parse_git_branch {
   git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
function gacm() {
 git acm "$*"
}

GIT_PS1_SHOWDIRTYSTATE=true
export LS_OPTIONS='--color=auto'
export CLICOLOR='Yes'
export LSCOLORS=gxfxbEaEBxxEhEhBaDaCaD

export PS1=$CYAN'\n\d '$LIGHT_GRAY'\A 💩 $(
   if [[ $(__git_ps1) =~ \*\)$ ]]
   # a file has been modified but not added
   then echo "'$YELLOW'"$(__git_ps1 " (%s)")
   elif [[ $(__git_ps1) =~ \+\)$ ]]
   # a file has been added, but not commited
   then echo "'$MAGENTA'"$(__git_ps1 " (%s)")
   # the state is clean, changes are commited
   else echo "'$CYAN'"$(__git_ps1 " (%s)")
   fi)'$YELLOW" \W "$CYAN"→ "$GREEN

alias dm="cd ~/DevMtn"
alias ..="cd .."
alias lsq='live-server -q'
alias ucp="uncommitted ~/DevMtn"
alias grv="git remote -v"
alias gs='git status'
alias sourcebp="source ~/.bash_profile"
