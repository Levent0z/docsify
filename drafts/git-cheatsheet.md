```sh
$ git config --local user.email USER@DOMAIN # Replace with your email
$ git config --local user.name "FIRST LAST" # Replace with your full name
```

```sh
$ git add * # adds most files, but not those that start with '.'
```


### Tags
```sh
$ git tag TAGNAME REF # Add tag
$ git tag -d TAGNAME # Delete local tag (from HEAD)
$ git push --delete origin TAGNAME # Delete remote tag
```


# Bash Profile Additions (~/.bash_profile)

```sh
alias glo='git log --oneline -n20'
function gl() {
  if [ -z $1 ]; then
    ARG=
  else
    ARG=-n$1
  fi
  git log --pretty=format:"%h%x09%an%x09%ad%x09%s" --date=iso $ARG
}
alias gs='git status'

function gf() {
  if git checkout master; then if git fetch upstream; then git rebase upstream/master; fi; fi
}

# Returns 1 if git branch has changes
function gd() {
  if [[ $(git status 2> /dev/null | tail -n1) != *"working tree clean"* ]]; then 
    return 1
  else
    return 0
  fi
}

function parse_git_dirty() {
  [[ $(git status 2> /dev/null | tail -n1) != *"working tree clean"* ]] && echo "*"
}

function parse_git_branch() {
  git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e "s/* \(.*\)/\1/"
}

function parse_git_branch_dirty() {
  git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e "s/* \(.*\)/\1$(parse_git_dirty)/"
}

function git_branch_text() {
  #outputs a text to use in export PS1 statement
  local gb=$(parse_git_branch)
  [[ -n "$gb" ]] && echo "$gb$(parse_git_dirty)"  
}

export PS1="\n\[\e[1;37m\]\t \[\e[1;33m\]\h \[\e[1;36m\]\w \[\e[1;31m\]\$(git_branch_text)\n\[\e[1;36m\]o>\[\e[0;37m\]"

#export GIT_SSH_COMMAND="ssh -i /Users/levent0z/.ssh/levent0z_id_rsa"

```
