# Bash Utils - Draft

## Prompt and read user input into a variable

```bash
read -p 'Please input your name: ' USER
read -sp 'Please input your password: ' PWD
```

## Get Date time

```bash
NOW=`date +"%Y%m%d_%H%M%S"`
```

## Protect against the last line not having a new line, while reading from a path

```bash
while read LINE || [ -n "$LINE" ]; do
    echo $LINE
done < "path/to/file" >/dev/null
```

## Ignore changes in the amount of white space

```bash
diff -b $FILE1 $FILE2
```

## Force kill

```bash
kill -9 <pid>
```

## Get Base64 token

This can be used with `npm config set` to set the `_auth` value in `.npmrc`.

```bash
echo -n 'username:password' | base64
```

## Use JavaScript for shell

[Reference](https://2ality.com/2011/12/nodejs-shell-scripting.html)

1. Put a `shebang` at the top of the file:
   ```bash
   #!/usr/bin/env node
   ```
2. Make the script executable:
   ```bash
   chmod u+x myscript.js
   ```

## Java Helpers 

```bash
jps -l # List Java Processes

jstack -l <java-pid> # Sample call stacks

/usr/libexec/java_home # Get location of the JDK
```

## Using [Termenu](https://github.com/elifiner/termenu)

```bash
$ echo -n "Would you like to exit? " && termenu -i Yes No Maybe
```

## Random find/grep nodes

```bash
grep -r expression .
```

```bash
while read LINE; do grep function $LINE; done <<< `find . -type f -name "*.js"`
```

```bash
find . -type f -name "*.js" | xargs grep function
find . -type f -name “*.js” | xargs -P4 grep expression # parallel execution, max 4 procs
```

dirname
basename
yes
```

```bash
nvm_get_os ()
{
    local NVM_UNAME;
    NVM_UNAME="$(command uname -a)";
    local NVM_OS;
    case "$NVM_UNAME" in
        Linux\ *)
            NVM_OS=linux
        ;;
        Darwin\ *)
            NVM_OS=darwin
        ;;
        SunOS\ *)
            NVM_OS=sunos
        ;;
        FreeBSD\ *)
            NVM_OS=freebsd
        ;;
        AIX\ *)
            NVM_OS=aix
        ;;
    esac;
    nvm_echo "${NVM_OS-}"
}
```

## Create folders and sub folders as needed

```bash
mkdir -p a/b/c
```

## Bash Prompt example:

```bash
export PS1="\n\[\e[1;37m\]\t \[\e[1;33m\]\h \[\e[1;36m\]\w \[\e[1;31m\]\$(git_branch_text)\n\[\e[1;36m\]o>\[\e[0;37m\]"
```

## Random Tips
- `local` is only usable inside a function, outside, prefer to use `declare`
- Use `cat` to conCATenate multiple files before sending to a processor like `terser` for JavaScript or `csso` for CSS.

## Get OS details on macOS
```bash
$ /usr/bin/sw_vers
ProductName:	Mac OS X
ProductVersion:	10.15.7
BuildVersion:	19H15
```

### Directory Service Command Line (dscl)

```bash
dscl # interactive mode, use cd to change directory, ls to list
dscl "/Active Directory/SFDC/All Domains" -list /Groups
dscl "/Active Directory/SFDC/All Domains" -read /Groups/CodeCollab
```

Another command to check out: `dscacheutil`

### Identity

```bash
$ id -nG loz # All groups loz is in
SFDC\Domain Users localdb everyone ....

$ dsmemberutil checkmembership -U loz -G "SFDC\Domain Users"
user is a member of the group
```



```
pkg=$(cat package.json) && echo <"$pkg"
```

---

### NPM Run

```bash
function npmrun() {
  echo OPTIONS
  # Show all key/value pairs in the "scripts" section, removing first and last lines
  cat package.json | jq .scripts | tail +2 | sed '$d'
  echo "SELECT TO RUN:" 

  # 1. List all keys of scripts object on one line, strip all double-quotes
  # 2. Replace new-lines in above's output with spaces and save it in a variable
  list=$(cat package.json | jq '.scripts | keys | .[]' | sed 's/"//g' | tr -s "\n" " ") 
  COLUMNS=1 
  select sel in $list
  do 
    npm run $sel
    break
  done
}
```

```bash
sudo passwd centos # change password for the user centos
```

```bash
$ tput rmam # Disable line wrapping
$ tput smam # Enable line wrapping
```

## Create Symbolic Links

If you run this script from the root of the project, it will create a new rootref folder that you can then include as an entry under directories in .bazelproject:

```bash
mkdir rootref; ls -1p | grep -v / | grep -v BUILD | grep -v bazel- | while read line; do bs=$(basename $line); ln -s $(pwd)/$bs $(pwd)/rootref/$bs; done
```

## Force RSA key for SSH-KEYGEN

Specify the `-m PEM` option:

```bash
ssh-keygen -t rsa -b 4096 -m PEM
```

## fzf

[YouTube](https://www.youtube.com/watch?v=qgG5Jhi_Els)

### Tips

- Prefix search text with a single quote to enable exact match
- Space-separated keywords (expressions) are ANDed
- Negate keywords by prefixing them with exclamation point
- keywords are case-insensitive by default

### Calling long list on selected items

```bash
fzf | xargs ls -l   # Use tab/shift-tab to select multiple items (must enable multi mode first)
```

### Go to folder of selected file

```bash
cd `fzf | xargs dirname`
```

### Set Preview options

```bash
fzf --preview='[[ $(file --mime {}) =~ binary ]] && echo {} is a binary file || (bat --style=numbers --color=always {} || cat {}) 2> /dev/null | head -300'
```

### Options

```bash
export PS_FORMAT="pid,ppid,user,pri,ni,vsz,rss,pcpu,pmem,tty,stat,args"

FD_OPTIONS="--follow --exclude .git --exclude node_modules"

#export FZF_DEFAULT_OPTS="--no-mouse --height 50% -1 --reverse --multi --inline-info --preview='[[ \$(file --mime {}) =~ binary ]] && echo {} is a binary file || (bat --style=numbers --color=always {} || cat {}) 2> /dev/null | head -300' --preview-window='right:hidden:wrap' --bind='f3:execute(bat --style=numbers {} || less -f {}),f2:toggle-preview,ctrl-d:half-page-down,ctrl-u:half-page-up,ctrl-a:select-all+accept,ctrl-y:execute-silent(echo {+} | pbcopy)'"
export FZF_DEFAULT_OPTS="--height 50% -1 --reverse --multi --inline-info --preview='[[ \$(file --mime {}) =~ binary ]] && echo {} is a binary file || (bat --style=numbers --color=always {} || cat {}) 2> /dev/null | head -300' --preview-window='right:hidden:wrap' --bind='f3:execute(bat --style=numbers {} || less -f {}),f2:toggle-preview,ctrl-d:half-page-down,ctrl-u:half-page-up,ctrl-a:select-all+accept,ctrl-y:execute-silent(echo {+} | pbcopy)'"

# Use git-ls-files inside git repo, otherwise fd
export FZF_DEFAULT_COMMAND="git ls-files --cached --others --exclude-standard I fd --type f --type l $FD_OPTIONS"
export FZF_CTRL_T_COMMAND="fd $FD_OPTIONS"
export FZF_ALT_C_COMMAND="fs --type d $FD_OPTIONS"

export BAT_PAGER="less -R"
```

Ctrl+R in bash: Reverse History search

## URL Decode using Python

```bash
alias purldecode='python2 -c "import sys, urllib as ul; prin
t ul.unquote(sys.stdin.read());"'
```

## Remove first and last characters

```bash
cat abc.txt | sed 's/^"//' | sed 's/"$//' > abc2.txt
```

## Find occurrences of the keyword `rimraf` in package.json in the current directory and below

```bash
find . -type f -name "package.json" | xargs grep rimraf
```

## Display contents of file.ext in current folder and immediate subfolders

```bash
find . -name file.ext -maxdepth 2 | xargs cat
```

## Find file or folders that contain keyword

```bash
find . | grep KEYWORD
```

## Get Folder sizes in kilobytes (-k) of all child folders (-d0) in the given pattern, sorted as numbers (-n) in reverse order (-r) using first column (-k1)

```bash
du -kd0 ~/sdb*/sdb* | sort -rnk1
```

## Assign default value to var

```bash
[[ -z $1 ]] && v1='default' || v1=$1
```

## Fail Fast with message

```bash
function chexit() {
    # Check and exit if last return value is not 0, after echoing the message provided as the first argument.
    [[ $? != 0 ]] && echo "$1" && exit 1
}
```

## Prompt for user input

```bash
read -p 'y/n ' RESP; [[ $RESP == 'y' ]] && echo 'y' || echo 'n'
```

## Make an HTTP POST

[curl](https://ss64.com/osx/curl.html)

```bash
curl -X POST \
    -x PROXYHOST:PORT \
    -k \
    DESINATION_URL \
    --data 'key1=value1' \
    --data 'key2=value2' \
    --data-urlencode 'key3=value3'
    --data-urlencode 'key4=value4'
```

## Time a command's duration

```bash
time
```

## Strip substrings from a variable

Example: Substitute https with nothing:

```bash
URL_WITHOUT_HTTPS=$( echo ${URL//https:} )
```

Example: Substitute https with http:

```sb
URL='https://blah' && echo ${URL/https/http}
```

## Create a multi-line file

Pick a keyword known not to exist in the contents of the file to be created, e.g. EOFKEY

```bash
cat << EOFKEY > FILENAME
LINE1
LINE2
...
EOFKEY
```

## More Utility Scripts

https://github.com/alrra/dotfiles/blob/main/src/os/utils.sh

## Grep replacement

`rg`

## Using sed to replace lines in place

```bash
sed -i '' -E 's/^REPLACETHIS.+$/WITHTHIS/g' FILENAME
```

## Sorted list of files (folders shown first, includes coloring)

```bash
script -q /dev/null ls -hpGol1 | sort
```

## Replace back-tick with newline?

```bash
sed $'s/`/\\\n/g'
```

## SSH using key example

```bash
alias sshvm='ssh -i ~/vm.key vm@IP.AD.DR.ESS'
```

## All function arguments but the first one:

- `"${@:2}"` - retains new lines
- `"${*:2}"` - runs all of the arguments together as a single argument with spaces

## List Functions

- `typeset -f`
- `typeset -F`

## POST file to a URL

```bash
curl -v -H"Content-Type:text/plain" -d "@sampleCoreEnvelope.txt" "http://localhost:3002/api/uitelemetry_csv"
```

## Count how many colors xterm actually supports
[xterm-color-count.sh](https://github.com/l0b0/xterm-color-count)
