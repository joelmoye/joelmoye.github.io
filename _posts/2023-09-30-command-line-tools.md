---
title: "Dedicated Command Line Tools"
date: 2023-09-30 00:00:00 -0500
categories: [Ubuntu, Linux, Command Line, Tools]
tags: [ubuntu, linux, command, line, tools, dedicated, apt, repository, remove, update]
---


The safe way to add or remove software repositories using the terminal is using the command `add-apt-repository`. For example:

```
sudo add-apt-repository ppa:libreoffice/ppa
```

will add the libreoffice Fresh PPA. Using the `-r` option removes it again:

```
sudo add-apt-repository -r ppa:libreoffice/ppa
```

This command is installed by default in Ubuntu.

Alternatively, to remove a ppa, you could install `ppa-purge`. Next to removing a PPA, that script will also automatically revert packages to their versions of the official Ubuntu software sources, or remove them if they are not available there. For example:

```
sudo ppa-purge ppa:libreoffice/ppa
```

**Manually changing `/etc/apt/sources.list`**

You can also manually edit `/etc/apt/sources.list` or `/etc/apt/sources.list.d` to add repositories, but then you need to know the correct syntax. See `man sources.list 5` to find information about the required format. `/etc/apt/sources.list.d` alows to add entries as separate files instead of as a section in `/etc/apt/sources.list`. Only files with the extension `.list` or `.sources` - which have different formats - are interpreted as individual entries. Other files are ignored. To remove a repository registered in this directory, delete its `.list` or `.sources` file.

**Graphical tool: "Software & Sources"**

Finally, also consider the graphical tool "Software & Updates". With this tool, you can enable and disable official software sources, and add, enable or disable third party PPA's using graphical dialogs. Also that tool is available by default in Ubuntu.