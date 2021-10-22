# ZSH

## [Startup files](https://zsh.sourceforge.io/Intro/intro_3.html)

- `.zshenv` - sourced on all invocations of the shell, unless the -f option is set. 
  - should contain commands to set the command search path, plus other important environment variables. 
  - should not contain commands that produce output or assume the shell is attached to a tty.
- `.zprofile` - meant as an alternative to `.zlogin' for ksh fans
  - .zlogin and .zprofile are not intended to be used together
- `.zshrc` - sourced in interactive shells.
  - should contain commands to set up aliases, functions, options, key bindings, etc.
- `.zlogin` - sourced in login shells. 
  - should contain commands that should be executed only in login shells. 
- `.zlogout` - sourced when login shells exit.

