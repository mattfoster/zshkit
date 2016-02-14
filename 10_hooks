# From: http://dotfiles.org/~_why/.zshrc
# Really works with minimal prompt setup.

short_hostname=$(hostname -s)

# format titles for screen and rxvt
function title() {
  # escape '%' chars in $1, make nonprintables visible
  a=${(V)1//\%/\%\%}

  # Truncate command, and join lines.
  a=$(print -Pn "%40>...>$a" | tr -d "\n")

  case $TERM in
  screen)
    print -Pn "\ek($short_hostname) $a:$3\e\\"      # screen title (in ^A")
    ;;
  xterm*|rxvt|ansi)    
    print -Pn "\e]1;$2 | $a:$3\a" # plain xterm title
    print -Pn "\e]2;$2 | $a:$3\a" # tab title
    ;;
  esac
}

# precmd is called just before the prompt is printed
function precmd() {
  # This may not be the best way of doing this.
  if is-at-least 4.2.6
  then
    vcs_info_msg_0_=$(git-prompt)
  elif [[ $git_enable == 1 ]]
  then
    vcs_info
  else
    vcs_info_msg_0_=''
  fi
  # This loads the info messgage into %1v.
  title "zsh" "$USER@$short_hostname" "%55<...<%~"
}

# preexec is called just before any command line is executed
function preexec() {
  title "$1" "$USER@$short_hostname" "%35<...<%~"
}

function postcmd() {
  title "$1" "$USER@$short_hostname" "%35<...<%~"
}
