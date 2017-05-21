---
layout: default
title: Chromebook SSH Setup
subtitle: Set up SSH access from a Chromebook to a WRT54g
permalink: /hsmm-mesh/chromebook-ssh-setup/
order: 2
comments: yes
---

## SSH Setup using Chromebook
This is a guide of how I set connected to my node over ssh from my Chromebook. Optional steps are installing `zsh`, `nano`, and creating an alias to assist it connecting

**1.** Open crosh **ctrl** + **alt** + **t**

**2.** Type `shell`

**3.** (optional) Install [Chrome Homebrew(crew)](https://skycocker.github.io/chromebrew/) `wget -q -O - https://raw.github.com/skycocker/chromebrew/master/install.sh | bash`

**4.** Install zsh `crew install zsh`

**5.** Close tab, or type `exit`.

**6.** Open crosh again **ctrl** + **alt** + **t**

**7.** UI should appear different now that zsh is running.

**8.** Generate SSH key `ssh-keygen -t rsa`

* Should suggest that you create the key at `/home/chronos/user/.ssh`
* Press **Enter**

**9.** Your key should now be generated. Check for the key by running `ls -al /home/chronos/user/.ssh`

**10.** Install the key on your node

* Since the ChromeOS file browser doesn't allow us to access any files outside of `Downloads` we need to copy our SSH key into the `Downloads` folder
* Run `cp /home/chronos/user/.ssh/id_rsa.pub ~/Downloads/id_rsa.pub`
* This command copies the file `id_rsa.pub` into your `Downloads` folder.
* Access your local node. Typically via [http://localnode:8080/cgi-bin/admin](http://localnode:8080/cgi-bin/admin)
* Select the `id_rsa.pub` file from the **Authorized SSH Keys** section

**11.** (optional) Setup an alias which will allow you to access ssh more easily

* `crew install nano` (because I hate vim)
* `nano ~/.zshrc`
* Use arrow keys to go to bottom of file
* Copy & Paste function hsmm-ssh() { ssh root@$1 -oKeyAlgorithms=+diffie-hellman-group1-sha1 -p2222 }
* **ctrl** + **x** to save. **ctrl** + **o** to exit

**12.** If you created the alias/function you can now type `hsmm-mesh localnode` to access your node via ssh. Alternatively, if you're accessing your node through another node, or through some other router you can type something like `hsmm-ssh 192.168.1.100` where the IP address is your host