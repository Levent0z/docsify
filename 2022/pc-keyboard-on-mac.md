# PC Keyboard on MacOS

If you have a PC-style keyboard with separate `home`, `end`, `page up` and `page down` keys, you've likely noticed they don't always work like you would expect on macOS, especially if you are used to the behavior in Windows. 

Thanks to [this blog](https://damieng.com/blog/2015/04/24/make-home-end-keys-behave-like-windows-on-mac-os-x/), it's easy to configure macOS to behave like that. 

In a terminal run the following:

```bash
function genKeyBindings() {
    mkdir -p ~/Library/KeyBindings
    cd ~/Library/KeyBindings
    if [[ -f DefaultKeyBinding.dict ]]; then
        read -p 'Confirm overwrite of existing key bindings to continue: (y/n) ' INPUT
        if [[ "$INPUT" != 'y' ]] && [[ "$INPUT" != 'Y' ]]; then
            echo 'Canceled.';
            return 1;
        fi
    fi

    cat << EOFKEY >DefaultKeyBinding.dict
{
"\UF729"  = moveToBeginningOfLine:; // home
"\UF72B"  = moveToEndOfLine:; // end
"$\UF729" = moveToBeginningOfLineAndModifySelection:; // shift-home
"$\UF72B" = moveToEndOfLineAndModifySelection:; // shift-end
"^\UF729" = moveToBeginningOfDocument:; // ctrl-home
"^\UF72B" = moveToEndOfDocument:; // ctrl-end
"^$\UF729" = moveToBeginningOfDocumentAndModifySelection:; // ctrl-shift-home
"^$\UF72B" = moveToEndOfDocumentAndModifySelection:; // ctrl-shift-end
}
EOFKEY

    [[ "$?" == "0" ]] && echo 'Done.' || echo 'Failed'.
}
genKeyBindings
```