setopt nobeep	            # No beeping
setopt AUTOPUSHD PUSHDMINUS PUSHDSILENT PUSHDTOHOME
setopt AUTOCD			    # cd by typing dirname
setopt cdablevars	        # Follow variables which are dirnames
setopt interactivecomments	# allow comments on cmd line.
# setopt SH_WORD_SPLIT      # split up var in "for x in *"
setopt MULTIOS			    # Allow multiple redirection echo 'a'>b>c
setopt CORRECT CORRECT_ALL	# Try to correct command line spelling
setopt BANG_HIST		    # Allow ! for accessing history 
setopt NOHUP			    # Don't HUP running jobs on logout.
setopt NOBGNICE             # Don't renice background jobs
setopt EXTENDED_GLOB        # Enable extended globbing

# TERM specific options

case $TERM in
screen)
  setopt ignore_eof
  ;;
xterm*|rxvt|ansi)    
  ;;
esac

zstyle ':completion:*' completer _expand _complete

zstyle ':completion:*' use-cache on
zstyle ':completion:*' users resolve
# use dircolours in completion listings
zstyle ':completion:*' list-colors ${(s.:.)LS_COLORS}
# Enable menu completion
zstyle ':completion*:default' menu 'select=1'

# allow approximate matching
zstyle ':completion:*' completer _complete _match _approximate
zstyle ':completion:*:match:*' original only
zstyle ':completion:*:approximate:*' max-errors 1 numeric
zstyle ':completion:*' auto-description 'Specify: %d'
zstyle ':completion:*' format 'Completing %d'
zstyle ':completion:*' verbose true
zstyle ':completion:*:functions' ignored-patterns '_*'
zstyle ':completion:*:*:(^rm):*:*files' ignored-patterns \
'*?.(o|c~|zwc)' '*?~'

# only java files for javac
zstyle ':completion:*:javac:*' files '*.java'

# no binary files for vi or textmate
zstyle ':completion:*:vi:*' ignored-patterns '*.(o|a|so|aux|dvi|log|swp|fig|bbl|blg|bst|idx|ind|out|toc|class|pdf|ps|pyc)'
zstyle ':completion:*:mate:*' ignored-patterns '*.(o|a|so|aux|dvi|log|swp|fig|bbl|blg|bst|idx|ind|out|toc|class|pdf|ps|pyc)'
zstyle ':completion:*:vim:*' ignored-patterns '*.(o|a|so|aux|dvi|log|swp|fig|bbl|blg|bst|idx|ind|out|toc|class|pdf|ps|pyc)'
zstyle ':completion:*:gvim:*' ignored-patterns '*.(o|a|so|aux|dvi|log|swp|fig|bbl|blg|bst|idx|ind|out|toc|class|pdf|ps|pyc)'
# no binary files for less
zstyle ':completion:*:less:*' ignored-patterns '*.(o|a|so|dvi|fig|out|class|pdf|ps|pyc)'
zstyle ':completion:*:zless:*' ignored-patterns '*.(o|a|so|dvi|fig|out|class|pdf|ps|pyc)'
# pdf for xpdf
zstyle ':completion:*:xpdf:*' files '*.pdf'
# tar files
zstyle ':completion:*:tar:*' files '*.tar|*.tgz|*.tz|*.tar.Z|*.tar.bz2|*.tZ|*.tar.gz'
# latex to the fullest
# for printing
zstyle ':completion:*:xdvi:*' files '*.dvi'
zstyle ':completion:*:dvips:*' files '*.dvi'
# Group relatex matches:
zstyle ':completion:*' group-name ''
zstyle ':completion:*:-command-:*:(commands|builtins|reserved-words-aliases)' group-name commands
# Separate man page sections
zstyle ':completion:*:manuals' seperate-sections true
# Separate comand line options and descriptions with #
zstyle ':completion:*' list-separator '#'
# Generate descriptions for arguments
zstyle ':completion:*' auto-description 'specify: %d'

# Give long completion options in a list. tab to advance.
zstyle ':completion:*:default' list-prompt '%S%M matches%s'

autoload -Uz compinit
compinit

bash_source() {
  alias shopt=':'
  alias _expand=_bash_expand
  alias _complete=_bash_comp
  emulate -L sh
  setopt kshglob noshglob braceexpand

  source "$@"
}

have() {
  unset have
  (( ${+commands[$1]} )) && have=yes
}

# Autoload some bash completion functions if they exist.
autoload -Uz bashcompinit
bashcompinit

if [[ -e /etc/bash_completion.d/ack-grep ]];then
  bash_source /etc/bash_completion.d/ack-grep
fi

autoload -Uz colors
colors

autoload -Uz is-at-least

if is-at-least 4.3.6; then
  autoload -Uz vcs_info
  zstyle ':vcs_info:*' disable cdv darcs mtn p4 svk tla
  zstyle ':vcs_info:*' enable git cvs svn hg bzr
  zstyle ':vcs_info:*' get-revision true
  zstyle ':vcs_info:*' formats '%b '
  zstyle ':vcs_info:(svn|bzr|cvs):*' branchformat '%b:%r'
  zstyle ':vcs_info:cvs:*' branchformat '%r '
  zstyle ':vcs_info:bzr:*' use-simple true 
  # vcs_info also needs to be in precmd, see: 10_hooks
  vcs_info
fi
# Needed for doc function in 03_help.
compdef _doc doc
# Set up completion for bundle function in 05_editor.
compdef _bundle bundle
