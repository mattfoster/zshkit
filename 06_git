if [[ -x `which git` ]]; then
	git_enable=1
	function git-branch-name () {
		git branch 2> /dev/null | grep '^\*' | sed 's/^\*\ //'
	}
  # Return 1 if repository is dirty. 0 if it isn't a repostory, or is clean.
	function git-dirty () {
	  local code
		gs=$(git status 2> /dev/null)
		if [[ $? == 128 ]];
		then
		  code=0
	  else
		 echo $gs | grep "nothing to commit (working directory clean)" | 2>&1 > /dev/null
		 code=$?
	 fi
		echo $code
	}
	function gsrb () {
		branch=$(git-branch-name) 
		git checkout master
		git svn rebase
		git checkout "${branch}"
		git rebase master
	}
	
	function git-toggle() {
		if [[ $git_enable = 1 ]]; then
			git_enable=0
		else
			git_enable=1
		fi
	}
	
  function git-prompt() {
    emulate -L zsh
    dirty_color=$fg[cyan]
    branch=$(echo $gstatus | head -n 1 | sed 's/^#\s*On branch //')
    if [[ $branch == '# Not currently on any branch.' ]]; then
      no_branch=1
      branch='none'
          fi
    if [[ $git_enable = 1 ]]; then
      gstatus=$(git status 2> /dev/null)
      branch=$(echo $gstatus | head -n 1 | sed 's/^On branch //')
      dirty=$(echo $gstatus | sed 's/^#.*$//' | tail -n 2 | grep 'nothing to commit (working directory clean)'; echo $?)
      if [[ x$branch != x ]]; then
        if [[ $dirty = 1 ]] { dirty_color=$fg[magenta] }
                  if [[ $no_branch = 1 ]] { dirty_color=$fg[red] }
        [ x$branch != x ] && echo "%{$dirty_color%}$branch%{$reset_color%} "
      fi
    else
      echo "%{$dirty_color%}!%{$reset_color%}"
    fi
  }
	
	function git-scoreboard () {
		git log | grep Author | sort | uniq -ci | sort -r
	}
	function git-track () {
		branch=$(git-branch-name)
		git config branch.$branch.remote origin
		git config branch.$branch.merge refs/heads/$branch
		echo "tracking origin/$tracking"
	}
	function github-init () {
		git config branch.$(git-branch-name).remote origin
		git config branch.$(git-branch-name).merge refs/heads/$(git-branch-name)
	}
	
	function github-url () {
		git config remote.origin.url | sed -En 's/git(@|:\/\/)github.com(:|\/)(.+)\/(.+).git/https:\/\/github.com\/\3\/\4/p'
	}
	
	# Seems to be the best OS X jump-to-github alias from http://tinyurl.com/2mtncf
	function github-go () {
		open $(github-url)
	}
	
	function nhgk () {
		nohup gitk --all &
	}

  alias g='git'
  alias gb='git branch -a -v'
  alias gs='git status'
  alias gd='git diff'
  alias gf='git fetch'
  alias gr='git-rebase'
  alias gsc='git-svn dcommit'
  alias gsr='git-svn rebase'
  alias gsf='git-svn fetch'
  # gc      => git checkout master
  # gc bugs => git checkout bugs
  function gc {
  if [ -z "$1" ]; then
    git checkout master
    else
    git checkout $1
  fi
  }
fi
