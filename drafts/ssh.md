# Shell to Remote Host

Local: 
Remote: loz-wsm

Note: Remove  entries for the REMOTEHOST from `~/.ssh/known_hosts`
Note: May need to flushdns
```bash
alias flushdns='sudo killall -HUP mDNSResponder; say dns cleared successfully'
```

```bash
REMOTEHOST='MYREMOTEHOST.MYDOMAIN.com' # Set this to the FQDN of your remote host
KEYNAME='id_rsa_local' # change this to your liking

cd $HOME/.ssh
ssh-keygen # specify the value of $KEYNAME as the filename, no passphrase
ssh-copy-id -i ./$KEYNAME.pub $REMOTEHOST # copies public key to remote machine's ~/.ssh/authorized_keys

alias sicp="scp -i $HOME/.ssh/$KEYNAME -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -o LogLevel=QUIET"
alias sish="ssh -i $HOME/.ssh/$KEYNAME -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -o LogLevel=QUIET"
```

## Example Usage: 
```bash
sicp ~/.bash_profile $REMOTEHOST:/Users/loz/
sish $REMOTEHOST
```

## Basic Copy Example
```bash
scp USERNAME@HOSTNAME:/Users/USERNAME/FILE* .
# Asks for password
# If 2FA is enabled, check your authenticator. If it times out, it will ask for "Verification Code"
```

## Misc
https://superuser.com/questions/141344/dont-add-hostkey-to-known-hosts-for-ssh

