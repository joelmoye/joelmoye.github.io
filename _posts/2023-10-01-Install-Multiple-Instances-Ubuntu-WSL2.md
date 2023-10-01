---
title: "How to install multiple instances of Ubuntu in WSL2"
created: 2023-10-01T06:10:55 (UTC -04:00)
categories: [Ubuntu, Linux, Command Line, Tools]
tags: [ubuntu,wsl,wsl2,linux,windows]
source: https://joelmoye.github.io/posts/Install-Multiple-Instances-Ubuntu-WSL2/
---
> ## Excerpt
> A guide to installing multiple fresh instances of Ubuntu in WSL2

---
Table of Contents

-   [Installing multiple instances of Ubuntu in WSL2](#installing-multiple-instances-of-ubuntu-in-wsl2)
    -   [Step 1: Install the latest version of Ubuntu in WSL2](#step-1-install-the-latest-version-of-ubuntu-in-wsl2)
    -   [Step 2: Download the Ubuntu WSL tarball](#step-2-download-the-ubuntu-wsl-tarball)
    -   [Step 3: Install the second instance of Ubuntu in WSL2](#step-3-install-the-second-instance-of-ubuntu-in-wsl2)
    -   [Step 4: Login to the second instance of Ubuntu in WSL2](#step-4-login-to-the-second-instance-of-ubuntu-in-wsl2)
    -   [Step 5: Setup user accounts](#step-5-setup-user-accounts)
    -   [Step 6: Configure default user](#step-6-configure-default-user)
    -   [Step 7: Login as the new user](#step-7-login-as-the-new-user)

Windows Subsystem for Linux 2 ([WSL2](https://docs.microsoft.com/en-us/windows/wsl/install)) is in its second iteration that uses an actual Linux Kernel, an upgrade of the previous kernel emulator which was called Windows Subsystem for Linux (WSL).

It's a great tool developers who need to Linux for developing and testings their apps. And sometimes, you just want more than one instance of Ubuntu on your machine.

## Installing multiple instances of Ubuntu in WSL2

If you are running windows 10 version 2004 or higher (Build 19041 and above), you can install the latest version of Ubuntu in WSL by running the the below command.

### Step 1: Install the latest version of Ubuntu in WSL2

This will take care of all the steps required, i.e.

1.  It will enable the optional compoenents required on windows (e.g. Windows Virtualisation Platform, etc.)
2.  Enable Windows Subsystem for Linux 2 (WSL2)
3.  Update the Linux kernel to the latest version
4.  Install the default Linux distribution, i.e. latest Ubuntu

Once installed, just run `wsl` to open the WSL2 shell, on the first login you will be asked to choose username and password.

### Step 2: Download the Ubuntu WSL tarball

You can download the Ubuntu WSL tarball from the [Ubuntu WSL2 Image](https://cloud-images.ubuntu.com/releases/hirsute/release/ubuntu-21.04-server-cloudimg-amd64-wsl.rootfs.tar.gz) and save it to your local machine.

You can use your Windows Terminal / Powershell to do so, first run the following command to remove `curl` alias which the mighty intelligent 🤡 Powershell developers have built in

Then, run the following command to download the Ubuntu WSL tarball. Copy paste the **entire code block** below into your Windows Terminal and run it

```
curl (("https://cloud-images.ubuntu.com",
"releases/hirsute/release",
"ubuntu-21.04-server-cloudimg-amd64-wsl.rootfs.tar.gz") -join "/") `
--output ubuntu-21.04-wsl-rootfs-tar.gz

```

If prompted with a warning, press "Paste anyway" and then press enter to execute. This will download the Ubuntu WSL image tarball to you current directory.

### Step 3: Install the second instance of Ubuntu in WSL2

Just the below command and

1.  Replace the `<Distribution Name>` with the name you want to give, e.g. `ubuntu-2`,
2.  Replace `<Installation Folder>` with the folder where you want to install the second instance of Ubuntu
3.  and finally replace `<Ubuntu Tarball path>` with the path of the Ubuntu WSL2 image tarball you downloaded earlier.

```
wsl --import <Distribution Name> <Installation Folder> <Ubuntu WSL2 Image Tarball path>

```

After that run, `wsl -l -v` to see the list of distributions installed.

### Step 4: Login to the second instance of Ubuntu in WSL2

To login you need to run:

```
wsl -d <Distribution Name>

```

### Step 5: Setup user accounts

Notice in the above image that the logged in user is a root account. So let's setup a normal user account.

First, while logged in to the second instance of Ubuntu in WSL2 as root, run the below command, replace `<USERNAME>` with the username of your choice:

Then, run the following command to create the user account and set the password:

```
useradd -m -G sudo -s /bin/bash "$NEW_USER"
passwd "$NEW_USER"

```

### Step 6: Configure default user

Next, we need to configure Ubuntu to log in as your new user by default instead of root.

To do so, run the below command: paste the entire block of code below into your teminal and press enter.

```
tee /etc/wsl.conf <<_EOF
[user]
default=${NEW_USER}
_EOF

```

### Step 7: Login as the new user

First, exit the WSL by running `logout`, then shutfown the second Ubuntu by running

```
wsl --terminate <Distribution Name>

```

Finally, login to the second instance of Ubuntu again:

```
wsl -d <Distribution Name>

```

##### Need Help? [Open a discussion thread on GitHub](https://github.com/joelmoye/joelmoye.github.io/discussions).


### Related Posts