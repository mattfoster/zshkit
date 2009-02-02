# From: http://dotfiles.org/~_why/.zshrc
# Really works with minimal prompt setup.

# format titles for screen and rxvt
function title() {
  # escape '%' chars in $1, make nonprintables visible
  a=${(V)1//\%/\%\%}

  # Truncate command, and join lines.
  a=$(print -Pn "%40>...>$a" | tr -d "\n")

  case $TERM in
  screen)
    print -Pn "\ek$a:$3\e\\"      # screen title (in ^A")
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
  if [[ $ZSH_VERSION < 4.3.7 ]]
  then
    vcs_info_msg_0_=$(git-prompt)
  elif [[ $git_enable == 1 ]]
  then
    vcs_info
  else
    vcs_info_msg_0_=''
  fi
  # This loads the info messgage into %1v.
  title "zsh" "$USER@%m" "%55<...<%~"
}

# preexec is called just before any command line is executed
function preexec() {
  title "$1" "$USER@%m" "%35<...<%~"
}

# Loads up .env.rc or .env files if there in the current tree.
# http://stackoverflow.com/questions/171563/whats-in-your-zshrc#211917
# cd -q is only available on new zsh versions. 
# i.e. it's in finks (4.5.6), but not Apple's (4.3.4)
# 
# WARNING: this breaks 'cd -', since it seems to change oldpwd to /.
# 
# if [[ $ZSH_VERSION > 4.3.4 ]]; then 
#   function chpwd; {
#   DIRECTORY="$PWD"
#   while true; do
#     if [ -f './.env.rc' ]; then
#       source './.env.rc'
#       break
#     fi
#     # Removed as it clashes with zshkit'szshenv.
#     # if [ -f './env' ]; then
#     #     source './env'
#     #     break
#     # fi
#     [ "$PWD" = '/' ] && break
#     cd -q ..
#   done
#   cd -q "$DIRECTORY"
#   }
# fi
