# Running Debian on Windows 10

- Install Debian distribution from the Windows App Store
- Create new tab in `Windows Terminal`

## Disable Chime for the terminal
```sh
echo 'set bell-style none' >> ~/.inputrc
```
Restart terminal

## Mounting and unmounting 

```sh
sudo mount -t drvfs E: /mnt/e
# sudo umount /mnt/e

sudo mount -t drvfs '\\HOST\PATH' /mnt/share
```
[More...](https://wiki.usask.ca/display/MESH/How+to+mount+and+unmount+Windows+drive+letters+and+network+locations+in+WSL
)
### Using CIFS

```sh
sudo apt update
sudo apt install cifs-utils
sudo mount.cifs //IPNUMBER/SHAR /mnt/SHARE -o user=USERNAME,pass=PASSWORD # Replace uppercase values
```

[More...](https://markontech.com/linux/mount-a-network-shared-drive-on-linux/)

## Reference

[Debian Reference](https://www.debian.org/doc/manuals/debian-reference/) - Includes tutorials