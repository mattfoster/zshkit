# Look for apt, and add some useful functions if we have it.
if [[ -x `which apt-get` ]]; then
  alias apt-get='noglob sudo apt-get'
  alias aptitude='noglob sudo aptitude'

  upgrade () {
  	if [ -z $1 ] ; then
  		sudo apt-get update
  		sudo apt-get -u upgrade
  	else
  		ssh $1 sudo apt-get update
  		# ask before the upgrade
  		local dummy
  		ssh $1 sudo apt-get --no-act upgrade
  		echo -n "Process the upgrade ?"
  		read -q dummy
  		if [[ $dummy == "y" ]] ; then
  			ssh $1 sudo apt-get -u upgrade --yes
  		fi
  	fi
  }
fi
