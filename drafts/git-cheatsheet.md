```sh
$ git config --local user.email USER@DOMAIN # Replace with your email
$ git config --local user.name "FIRST LAST" # Replace with your full name
```

```sh
$ git add * # adds most files, but not those that start with '.'
```

```sh
$ git remote -v
$ git remote add upstream 
```

```sh
$ git pull
...
Automatic merge failed; fix conflicts and then commit the result.
$ git merge --abort
,,,


### Tags
```sh
$ git tag TAGNAME REF # Add tag
$ git tag -d TAGNAME # Delete local tag (from HEAD)
$ git push --delete origin TAGNAME # Delete remote tag
```


### Diffing
```sh
$ git difftool HEAD~1 HEAD
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


#export GIT_SSH_COMMAND="ssh -i /Users/levent0z/.ssh/levent0z_id_rsa"

```


# Cherry-Pick from another branch
```sh
# First add the remote to the source branch. If the repo is on local, use absolute path for REPOURL
$ git remote add REMOTELABEL REPOURL
$ git fetch REMOTELABEL
# Switch to the git branch you want to cherry-pick into, use -b if crating new branch:
$ git checkout TARGETBRANCH
$ git cherry-pick SHA
# If there are merge conflicts, fix them in a code editor, add them with `git add` and then:
$ git cherry-pick --continue
```

# GPG

```sh
brew install gnupg
gpg --full-generate-key   // Use 4096 byte size
gpg --list-keys --keyid-format LONG
gpg --armor --export keyID
# Next, copy output with begin/end terminators into GitHub
```
