Matt Foster's zshkit fork
-------------------------

An easily extensible collection of `stuff` for zsh.

## Prompt info

I've included my prompt, 'Minimal VCS. As the name suggests this is a minimal
prompt with VCS information via `vcs_info`. For this to work, you'll need a
version zsh > 4.3.6 (IIRC). 

See `func/minimal_vcs_setup` for details, or run:

    autoload promptinit && promptinit
    prompt -h minimal_vcs

Proper functioning requires the 10_hooks to be loaded too, since `vcs_info`
must be run to update the prompt. It's also so minimal that you'll probably
want useful the useful information included in the title function.

## Current issues:

* I haven't found a way to easily show when the repo is dirty.
* I keep seeing bits and bobs alluding to a 'new prompt colour' syntax, but I can't find any docs.
