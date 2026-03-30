---
theme: csc-eurocc-2019
lang: en
---

# Connecting to CSC Supercomputers {.title}

This topic is about how to login to the CSC supercomputers.

<div class="column">
![](https://mirrors.creativecommons.org/presskit/buttons/88x31/png/by-sa.png)
</div>
<div class="column">
<small>
All materials (c) 2020-2026 by CSC – IT Center for Science Ltd.
This work is licensed under a **Creative Commons Attribution-ShareAlike** 4.0
Unported License, [http://creativecommons.org/licenses/by-sa/4.0/](http://creativecommons.org/licenses/by-sa/4.0/)
</small>
</div>

# Login via the web interfaces

- The easiest way to login to Roihu supercomputer is via [roihu.csc.fi](https://www.roihu.csc.fi)
- Login requires 1) [multi-factor authentication](https://docs.csc.fi/accounts/mfa/) (MFA) and 2) a medium or high level of identity assurance (LoA)
  - Haka is recommended if your home organization already requires MFA. Otherwise, [activate CSC MFA in MyCSC](https://my.csc.fi/mfa-activation-login) and use your CSC credentials
  - Check your LoA in [MyCSC](https://my.csc.fi/profile) and [elevate it if needed](https://docs.csc.fi/accounts/strong-identification)
- The web interface can be used, _e.g._, to launch GUI applications, browse files or open a command-line shell
   - The latter is useful if your computer does not have an SSH client, but you need command-line access to the supercomputer
- LUMI also has a [similar web interface](https://docs.lumi-supercomputer.eu/runjobs/webui/).

# Login with SSH (1/3)

- SSH is a terminal program that gives you command-line access on the CSC supercomputer
- It is a versatile main interface to a supercomputer
   - Laptop &harr; Toyota, Supercomputer &harr; F1. F1 needs a specialist interface.
- Logging in with SSH requires **SSH keys** and a valid **SSH certificate**
  - A key pair is created and the **public** key is uploaded to MyCSC
  - The public key must then be signed **every 24 hours** to obtain a time-based certificate allowing SSH logins to Roihu
  - Read the [documentation](https://docs.csc.fi/computing/connecting/ssh-keys/) and do the [tutorial](https://csc-training.github.io/csc-env-eff/hands-on/connecting/ssh-keys.html)
  - Consult the [FAQ](https://docs.csc.fi/support/faq/ssh-keys-not-working/) or contact <servicedesk@csc.fi> to troubleshoot issues

# Login with SSH (2/3)

- After adding your public key to MyCSC, you need to sign it to generate an SSH certificate
   - The [CSC certificate helper tool](https://github.com/CSCfi/certificate-helper-tool) is recommended
     - `python3 csc_cert.py -u <username> <path-to-local-public-key>`
     - Signs the key, downloads the certificate, and adds it to your _SSH agent_ to make logging in easy
     - Python is required on all operating systems.
     - Authentication agent also requires `ssh-agent` utility (Linux/macOS/PowerShell) **or** Pageant & WinSCP (PuTTY users).

# Login with SSH (3/3)

- After adding your public key to MyCSC, you need to sign it to generate an SSH certificate
   - The [CSC certificate helper tool](https://github.com/CSCfi/certificate-helper-tool) is recommended
   - `python3 csc_cert.py -u <username> <path-to-local-public-key>`
   - Signs the key, downloads the certificate, and adds it to your _SSH agent_ to make logging in easy
   - Python is required on all operating systems. To add the certificate to authentication agnet
- Detailed instructions for [logging in with SSH on macOS and Linux](https://docs.csc.fi/computing/connecting/ssh-unix/) and [on Windows](https://docs.csc.fi/computing/connecting/ssh-windows/)
  - On Windows, we recommend MobaXterm or PuTTY clients, or simply using the web interfaces instead of SSH
- Note! Plain SSH will not allow displaying remote graphics
   - The web interfaces are often best for this, but a graphical connection can also be enabled over SSH using [X11 forwarding](https://docs.csc.fi/computing/connecting/#graphical-connection)

# Moving files between a local computer and Roihu

- [`scp`](https://docs.csc.fi/data/moving/scp/) and [`rsync`](https://docs.csc.fi/data/moving/rsync/) are powerful command-line tools to copy files
   - `scp` works even in Windows PowerShell (but `rsync` is missing)
   - _e.g._ `scp filename cscusername@puhti.csc.fi:/scratch/project_xxxx`
   - _e.g._ `rsync -r foldername cscusername@puhti.csc.fi:/scratch/project_xxxx`
   - `rsync` exists in _MobaXterm_ but it removes write permissions of copied files
- Sometimes a [GUI tool for transferring files](https://docs.csc.fi/data/moving/graphical_transfer/) is more convenient
   - Nice tools are _e.g._ _FileZilla_ and _WinSCP_
   - _MobaXterm_ also has a file transfer GUI (Tip: set persistent home directory)
   - The web interfaces can also be used to easily upload/download files
- Note! Both the command-line and graphical file transfer tools are inherently SSH-based, so using them at CSC requires SSH keys!

# Moving files between Puhti and Roihu (1/2)

- SSH keys should be set up on your local computer
- To access Mahti from Puhti, or vice versa, you must ensure your SSH keys are *forwarded* to the server from where you want to connect onward
  - This is called _SSH agent forwarding_
  - Allows using e.g. `rsync` or `scp` to move files directly between Puhti/Mahti
- On Linux/macOS, add option `-A` to your SSH command
  - Example: `ssh -A cscusername@puhti.csc.fi`

# Moving files between Puhti and Roihu (2/2)

- Using MobaXterm:
  - Similar to Linux/macOS if using local terminal, otherwise toggle _Allow agent forwarding_ under "Session" -> "SSH" -> "Advanced SSH settings" -> "Expert SSH settings"
- Using PuTTY:
  - Select "SSH" -> "Connection" -> "Auth" and toggle option _Allow agent forwarding_ under "Other authentication-related options"
