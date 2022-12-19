# Setting up a Node server running on Synology Diskstation

I want to host my [my website](https://www.leventoz.com) on my Synology Diskstation(NAS). This will allow me to have a website rich with functionality such as server-side rendering and API support. I also want ease of development, full control over the site and not have to pay hosting fees.

So how do I set it up? I will explain the steps below. 

## 1. On the NAS:

Go to the Control Panel > Shared Folder
1. Click Create
2. Specify a name for the folder, e.g. `node-server`. This will be the network share name.
3. Accept the defaults as applicable.
4. This will create a folder in what was specified in the Location field. By default, this is "Volume 1: Btrfs", and the folder will be created under `/volume1`.

   
## 2. On local (the development machine):

We would like to mount the NAS folder locally so we can work with files easily. 

1. Open a terminal, and put int the following commands, replacing placeholders indicated in uppercase with values that apply to your config.
    ```bash
    mkdir -p ~/HOSTNAME/SHARE
    cd ~/HOSTNAME/SHARE
    mount -t smbfs //USERNAME@HOSTNAME/SHARE . # Put in password when prompted
    ```

   - HOSTNAME is the name of the NAS on the LAN
   - USERNAME is the name of a NAS user with admin access
   - SHARE is the name of the folder you shared in the previous section

    Once the mount succeeds, we can work on the files on NAS as if they're on our local.

2. Let's create the folder structure we will need:
    ```bash
    mkdir cert # This is where we will put SSL certificate files
    mkdir web # This is where we will put the Node files
    cd web
    ```

3. You can now proceed copying your node service files to the `web` folder.



## 3. Set up Remote Terminal

It will be necessary to open a remote terminal to the NAS to start the node server. To configure it:

1. **On the NAS**, go to Control Panel > Terminal & SNMP
2. Select the Terminal Tab
3. Check Enable SSH Service
4. Set Port to `220`.
5. Optionally set the Advanced Settings and reduce security if you get connection problems. Medium works for me.
6. **On local**, open a terminal and do:
    ```sh
    ssh HOSTNAME -p 220 
    # From this point on, the commands are executed on the remote machine
    cd /volume1/SHARE
    ```
7. Make a note of the installed versions of NPM and Node:
    ```sh
    node --version
    npm --version 
    ```
8. To go back to the local terminal, enter `exit`.


## 4. Working Locally

Often, it's more convenient to run the service on your local dev machine than NAS, especially if you want to set breakpoints. Because your local machine may have different versions of Node and NPM than Diskstation, we need to synchronize them.

Let's use [Volta](https://volta.sh/) for this purpose. I found this necessary because my local versions are much more recent than those of the Diskstation.

On your local, do:

```bash
curl https://get.volta.sh | bash # download Volta
cd ~/HOSTNAME/SHARE/web # Go to the folder where you have your Node project
volta pin npm@12.22.12
volta pin node@6.14.16
```

This will download the necessary versions and add the following in your `package.json`:
```json
"volta": {
    "node": "12.22.12",
    "npm": "6.14.16"
}
```

That's it. To add SSL to your web service, check out [Part 2](nas-node-ssl.md) of this blog post.


Note: I would be remiss if I didn't mention [NodeJS 4 Synology NAS](https://github.com/StephanThierry/nodejs4synologynas), which I referenced to get started.
