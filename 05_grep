if [[ -x `which ggrep` ]]; then
	alias rgrep=`which grep`
	alias grep='ggrep --color'
fi

output=$(GREP_OPTIONS=test grep --version 2>&1)

if [[ $output == ".*GREP_OPTIONS.*" ]]; then
# From zsh-lovers: detect gnu grep:
        (grep --help 2>/dev/null |grep -- --color) >/dev/null && \
        export GREP_OPTIONS='--color=auto'
fi
