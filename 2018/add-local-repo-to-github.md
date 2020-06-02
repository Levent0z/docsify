# How to Add Your Existing Local Git Repo to GitHub

<details><summary style="font-size:1.5em">Prologue</summary>
<p>It's super easy to clone a GitHub repo to your local environment. However, what if you started working on a simple project on your local, perhaps as an exercise or a proof-of-concept and now you want to push your work to GitHub into a new repo?</p>

<p>This path is not as straight-forward. Sure, you can brute-force your way, by creating and cloning a GitHub repo as usual, copying all your files, making a commit and pushing that. Although this will work, it's not the best approach. If you already had a Git repo locally, you will lose your Git History. </p>

<p>Here, I will show you a better way. If, like me, you have multiple GitHub accounts you may hit some roadblocks. Your GitHub account and your local environment must be properly configured, and that Git must be using the correct configuration.</p>
</details>

## TL;DR
This post walks you though the less-common path of pushing your local changes to a brand new GitHub repo (as opposed to pushing to a GitHub repo that you'd cloned from). It also touches on how to manage multiple GitHub accounts in the Troubleshooting section at the bottom.

> **Note**: I use the term **console** to refer to Command Prompt on Windows and Terminal on MacOS.

1. Sign-in to your [GitHub](https://github.com) account
2. Click `New Repository`
3. Give your repository a name unique in your account. 
4. **Do not** check `Initialize this repository with a README`.
5. **Do not** `Add .gitignore` and **do not** `Add a license`.
6. Click `Create Repository`.
7. Copy the SSH link to the clipboard.
8. If your local folder is not preinitialized as a git repo, use the console to do the following. Otherwise, skip this step.
    ```bash
    git init # initialize folder as a git repo 
    git add * # Assuming you already have a .gitignore file (copy one from another repo if not)
    git commit -m "Add all files"
    ```

9. In the console, do the following:

    ```bash
    git remote add origin SSHLINK_PLACEHOLDER # Replace the SSHLINK_PLACEHOLDER with the SSH link for your GitHub repo.
    git push -u origin master
    ```
---

## Troubleshooting

Although the instructions above are pretty straightforward, in practice there's many things that can go wrong. One example error message you might get is `Please make sure you have the correct access rights and the repository exists.`. Here are some ideas for troubleshooting.


### 1. Ensure user name and email are set
```bash
git config --global --list # Lists all set global configuration settings
git config --local --list # Lists all set local (per repo) configuration settings
```
I like to set my user email and name are set globally:
```bash
git config --global user.email YOURNAME@YOURDOMAIN.COM # Replace placeholder with your email address
git config --global user.name "FIRST LAST" # Replace placeholder with your full name.
```

### 2. Check Git remotes and spelling errors
The `remotes` for a repo are key-value pairs which instruct git to the location indicated by that keyword. `origin` should be pointing to the SSH link of your repo. This should go without saying, but check, double-check and triple-check that you're using the correct SSH link. This one once probably cost me an hour to figure out.

```bash
git remote -v
```

### 3. Ensure SSH keys are configured for your repo and your environment
1. On GitHub, go to `Settings` in the drop-down menu of your profile icon at the top-right.
2. In the left menu, select `SSH and GPG keys`.
3. If there's no entry for your machine, you need to create one in the console using **`ssh-keygen`** command. 

    You can use the `which` or `where` commands in Windows and MacOS respectively to figure out where this command is, if it's in the path. For my Windows 10 PC, it was in the following places:
    - C:\Windows\System32\OpenSSH\ssh-keygen.exe
    - C:\Program Files\Git\usr\bin\ssh-keygen.exe  <-- This must have been installed with `Git for Windows`.

    When ssh-keygen asks you where to save the files, you can specify the default unless you have multiple GitHub accounts. If that's the case, simply specify the full-path and provide a filename that indicates the account for easy reference. See the next troubleshooting item for more information.

4. Go to the folder where the SSH files are saved (typically `.ssh` in your user folder). Open the `.pub` file in a text editor and copy **all** of the text to the clipboard.
5. Go to GitHub, click `New SSH key`, and paste in the `Key` field. I like to set the `Title` to remind me which machine I'm using this key.


### 4. Use the correct RSA key files for SSH (aka `git push` as a different user)

If you have multiple GitHub accounts, make sure that you're using the correct RSA files. The defaults may not be correct depending on your account. One way to do this is to set the environment variable `GIT_SSH_COMMAND` so that it instructs SSH to use the correct (private) key file.

On Windows:
```dos
@REM Replace the placeholder below with the path and name of your rsa file, eg. "C:\Users\LeventOz\.ssh\id_rsa"
set GIT_SSH_COMMAND=ssh -i "\SOMEPATH\RSA_PRIVATE_KEY_FILENAME"
```
On MacOS:
```bash
export GIT_SSH_COMMAND="ssh -i /SOMEPATH/RSA_PRIVATE_KEY_FILENAME" # Replace the placeholder, eg. /Users/leventoz/.ssh/key
```

> **Tip**: to see which username an RSA file points to, use the following command: (Example is on Windows, for MacOS use forward slashes):
> ```dos
> ssh -T -ai \SOMEPATH\RSA_PRIVATE_KEY_FILENAME git@github.com
> ```
