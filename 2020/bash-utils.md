
Prompt and read user input into a variable
```sh
read -p 'Please input your name: ' USER
read -sp 'Please input your password: ' PWD
```

Get Date time
```sh
NOW=`date +"%Y%m%d_%H%M%S"`
```

# Protect against the last line not having a new line, while reading from a path
```sh
while read LINE || [ -n "$LINE" ]; do
    echo $LINE
done < "path/to/file" >/dev/null
```

# Ignore changes in the amount of white space
```sh
diff -b $FILE1 $FILE2
```

# Force kill
```sh
kill -9 <pid>
```

# Get Base64 token

```sh
echo -n 'username:password' | base64
```

# Use JavaScript for shell

[More Info](https://2ality.com/2011/12/nodejs-shell-scripting.html)

1. Put a shebang at the top of the file:
    ```sh
    #!/usr/bin/env node
    ```
2. Make the script executable:
    ```sh
    chmod u+x myscript.js
    ```

# List Java Processes

```sh
jps -l
```

# Sample call stacks
```sh
jstack -l <java-pid> 
```


https://github.com/elifiner/termenu
Can install through gitter (linked)

$ echo -n "Would you like to exit? " && termenu -i Yes No Maybe

o>/usr/libexec/java_home
/Library/Java/JavaVirtualMachines/sfdc-openjdk_11.0.8_11.41.54.jdk/Contents/Home


grep -r expression .

while read LINE; do grep function $LINE; done <<< `find . -type f -name "*.js"`

find . -type f -name "*.js" | xargs grep function
find . -type f -name “*.js” | xargs -P4 grep expression # parallel execution, max 4 procs


find ~/blt/app/228/patch/core/ext -type d -name "org.apache_*"


dirname
basename
yes

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


mkdir -p a/b/c



export PS1="\n\[\e[1;37m\]\t \[\e[1;33m\]\h \[\e[1;36m\]\w \[\e[1;31m\]\$(git_branch_text)\n\[\e[1;36m\]o>\[\e[0;37m\]"


`local` is only usable inside a function, outside, prefer to use `declare`


Use cat to conCATenate multiple files before sending to a processor like `terser` for JavaScript or `csso` for CSS.


o>/usr/bin/sw_vers
ProductName:	Mac OS X
ProductVersion:	10.15.7
BuildVersion:	19H15


Directory Service Command Line (dscl) 

dscl # interactive mode, use cd to change directory, ls to list
dscl "/Active Directory/SFDC/All Domains" -list /Groups
dscl "/Active Directory/SFDC/All Domains" -read /Groups/CodeCollab

dscacheutil

$ id

$ id -nG loz # All groups loz is in
SFDC\Domain Users localdb everyone ....

$ dsmemberutil checkmembership -U loz -G "SFDC\Domain Users"
user is a member of the group

---

pkg=$(cat package.json) && echo <"$pkg"

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

```sh
sudo passwd centos # change password for the user centos
```

```sh
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
```sh
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

```sh
fzf | xargs ls -l   # Use tab/shift-tab to select multiple items (must enable multi mode first)
```

### Go to folder of selected file
```sh
cd `fzf | xargs dirname`
```

### Set Preview options
```sh
fzf --preview='[[ $(file --mime {}) =~ binary ]] && echo {} is a binary file || (bat --style=numbers --color=always {} || cat {}) 2> /dev/null | head -300'
```

### Options

```sh
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

```sh
alias purldecode='python2 -c "import sys, urllib as ul; prin
t ul.unquote(sys.stdin.read());"'
```

## Remove first and last characters

```sh
cat abc.txt | sed 's/^"//' | sed 's/"$//' > abc2.txt
```

## Find occurrences of the keyword `rimraf` in package.json in the current directory and below
```sh
find . -type f -name "package.json" | xargs grep rimraf
```


## Display contents of file.ext in current folder and immediate subfolders
find . -name file.ext -maxdepth 2 | xargs cat

## Get Folder sizes in kilobytes (-k) of all child folders (-d0) in the given pattern, sorted as numbers (-n) in reverse order (-r) using first column (-k1)
```sh
du -kd0 ~/sdb*/sdb* | sort -rnk1
```


## Assign default value to var
[[ -z $1 ]] && v1='default' || v1=$1

## Ask
read -p 'y/n ' RESP; [[ $RESP == 'y' ]] && echo 'y' || echo 'n'


## Make an HTTP POST
[curl](https://ss64.com/osx/curl.html)

```sh
curl -X POST \
    -x PROXYHOST:PORT \
    -k \
    DESINATION_URL \
    --data 'key1=value1' \
    --data 'key2=value2' \
    --data-urlencode 'key3=value3' 
    --data-urlencode 'key4=value4'


## Time a command's duration
```sh
time
```