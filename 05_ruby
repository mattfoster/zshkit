#
# Set up ruby
#
autoload -U get-ruby-version && get-ruby-version

# If you alias ruby to (say) ruby 1.9, this should update irb too.
# You might want to alias 'gem' here too, if you do, remember to update your path.
local irb_options="--readline -r irb/completion"

if [[ -x $(which irb$RUBY_VERSION) ]]; then
  alias irb='irb$RUBY_VERSION $irb_options'
else
  alias irb="irb $irb_options"
fi

export RI='-f ansi --width 70'

if [[ -x `which fri` ]]; then
  alias ri=fri
fi
