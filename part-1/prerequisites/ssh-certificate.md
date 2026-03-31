---
layout: default
title: Working with SSH certificates
parent: 1. Prerequisites
grand_parent: Part 1
nav_order: 3
permalink: /hands-on/connecting/ssh-certificate.html
---

# Working with SSH certificates

> ‼️ To begin, make sure you have a user account at CSC that is a member of a project which has access to the Roihu and Allas services. Note that there’s a small delay before one can login to Roihu after creating a new project and adding services.
>
> 💬 SSH keys and certificates improve security and ease-of-use. They are required to be able to log in to Roihu from the terminal using an **SSH client**.
>
> ☝🏻 SSH keys and certificates are **not** necessary if you only use the browser-based web interfaces to log in to Roihu.
>
> ‼️ Before starting this tutorial, make sure you have [set up your SSH keys](ssh-keys.md).

## Option 1: Using the CSC certificate helper tool

💬 CSC has developed a Python helper tool for signing and downloading an SSH certificates, and adding it to your SSH agent.

💡 This is the recommended way to get your SSH certificate for logging in to Roihu using an SSH client!

### Windows

1. Check if you have Python installed on your computer:
   2. Open PowerShell or MobaXterm terminal.
   3. Type `python3` and hit `Enter`.
   4. If this opens a Python interpreter, you're good to go!
   5. If you get an error, you need to install Python. [Python downloads are available here](https://www.python.org/downloads/).
      - This may require admin privileges, so please be in contact with your local IT-support if necessary.
      - If Python for some reason cannot be installed on your computer, [please proceed with Option 2 instead](#option-2-manually-signing-and-downloading-certificate-in-mycsc).
2. [Download the certificate helper tool here](https://raw.githubusercontent.com/CSCfi/certificate-helper-tool/refs/heads/main/csc_cert.py) (right-click link and select _Save Link As..._).
3. Optional, but **strongly recommended**: Make sure you have an **SSH authentication agent** running.
   1. **Pageant** & **WinSCP** will enable automatic adding of SSH keys and certificates to Pageant SSH agent.
      - This is recommended for users logging in to Roihu using **PuTTY** or **MobaXterm GUI**.
      - Pageant comes bundled with both PuTTY and WinSCP installations. [Instructions for installing WinSCP are available here](https://winscp.net/eng/docs/installation).
   2. `ssh-agent` utility will enable adding automatic adding of SSH keys and certificates OpenSSH agent.

### Linux/macOS

## Option 2: Manually signing and downloading certificate in MyCSC

### Windows

### Linux/macOS

## More information

💭 Docs CSC: More information about [connecting](https://docs.csc.fi/computing/connecting/) and [SSH keys](https://docs.csc.fi/computing/connecting/ssh-keys/).
