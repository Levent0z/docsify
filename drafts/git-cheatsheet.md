```bash
$ git config --local user.email USER@DOMAIN # Replace with your email
$ git config --local user.name "FIRST LAST" # Replace with your full name
```

```bash
$ git add * # adds most files, but not those that start with '.'
```

```bash
$ git remote -v
$ git remote add upstream
```

```bash
$ git pull
...
Automatic merge failed; fix conflicts and then commit the result.
$ git merge --abort
```

### Tags

```bash
$ git tag TAGNAME REF # Add tag
$ git tag -d TAGNAME # Delete local tag (from HEAD)
$ git push --delete origin TAGNAME # Delete remote tag
```

### Diffing

```bash
$ git difftool HEAD~1 HEAD
```

# Bash Profile Additions (~/.bash_profile)

```bash
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

```bash
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

```bash
brew install gnupg
gpg --full-generate-key   // Use 4096 byte size
gpg --list-keys --keyid-format LONG
gpg --armor --export keyID
# Next, copy output with begin/end terminators into GitHub
```

# Turn of GPG commit signing locally

git config commit.gpgsign false

## Troubleshooting with GPG

-   [gpg failed to sign the data](https://stackoverflow.com/questions/41502146/git-gpg-onto-mac-osx-error-gpg-failed-to-sign-the-data/55646482#55646482)

# GitHub Markdown

To create an anchor to a heading in github flavored markdown. Add - characters between each word in the heading and wrap the value in parens (#some-markdown-heading) so your link should look like so:
[Heading Example](#heading-example)

# To reset the folder back to factory-settings (i.e. remove generated folders)

```bash
git clean -fdx
```

# Clone via HTTPS & Personal Access Token

1. In GitHub.com, go to your User > Settings > Developer settings > Personal access tokens
2. Generate new token, copy the text
3. You can now do:

    ```bash
    git clone https://USERNAME:PERSONALACCESSTOKEN@GITHOST/ORG/REPO.git
    ```

# Deep-Clean

```bash
git clean -n -dX # Dry run
git clean -f -dX # The real thing (include untracked files and folders)
```

Also, check out using `-dx` argument instead.

# Restore a file after it has been deleted

```bash
git rev-list HEAD -- FILENAME -n 1  # get the SHA for the latest commit that changed FILENAME
git checkout SHA^ FILENAME # Get the file from the last commit before the SHA
```

# Clone as user with token

```bash
git clone https://$SOME_USER:$SOME_TOKEN@GITHUBHOST/ORG/REPO.git --branch BRANCH PATH
```

# "Cherry-pick" from a repo on a different repo

Suppose you have two local clones of a git repo. One of them is a clone of a branch that belongs to someone else's fork, and the other is yours. What happens if you can't or shouldn't (force) push to their branch?

You can "cherry-pick" the changes to your own branch and do what you will. But how? You can't `git cherry-pick` across different repos. Instead, you use **patches**. First you `format-patch` on the source repo, then you apply the patches on the destination repo.

So suppose you do `git log --oneline -n20` and see that the source repo has the following recent commits:

```
b3bc5218e (HEAD -> otherBranch) commit msg 6
201f7e32e commit msg 5
cdc5a755c commit msg 4
dd130e601 commit msg 3
7283bc2aa commit msg 2
87cfe898c commit msg 1
714ae42b0 (master)
...
```

And the destination has the following:

```
714ae42b0 (HEAD -> ownBranch, origin/master, origin/HEAD, master)
ff53f12bd
10a17b1d7
cf42322ad
47283d642
...
```

Notice that the other branch is already rebased, and that the two branches share the commit with hash **714ae42b0**. In this case, you do the following in the folder of the otherBanch:

```bash
git format-patch 714ae42b0...b3bc5218e
```

This will create a set of **.patch** files for each commit in the current folder (e.g. 0001-commit-msg-1.patch)

Note that when specifying the range, we are specifying the start hash of the common commit, which is excluded.

Next, go to the other folder and do:

```bash
git am ../other/branch/\*.patch
```

This will commit the patches in the correct order. If you run into any issues, you can do `git am --abort`.


## Force Push Safely

```sh
git push --force-with-lease
```

Unlike `--force`, `--force-with-lease` won't push if there are commits in the remote branch that would be lost.

