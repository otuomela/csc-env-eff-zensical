---
layout: default
title: Modules in Roihu
parent: 4. Module system
grand_parent: Part 1
nav_order: 1
permalink: /hands-on/modules/modules-roihu.html
---

# Modules in Roihu

> ☝🏻 This tutorial requires that you have a [user account at CSC](https://docs.csc.fi/accounts/how-to-create-new-user-account/) that is a member of a project that [has access to the Roihu service](https://docs.csc.fi/accounts/how-to-add-service-access-for-project/).
>
> ☝🏻 You must also have [set up SSH keys and downloaded an SSH certificate that is still valid](../prerequisites/ssh-keys.md).

## Checking the default modules

1. Log in to Roihu-CPU with your user credentials (SSH or [Roihu web interface](https://www.roihu.csc.fi)):

   ```bash
   ssh <username>@roihu-cpu.csc.fi    # replace <username> with your CSC username, e.g. myname@roihu-cpu.csc.fi
   ```

2. Try a `module` command! Check out which modules are loaded as default as you login to Roihu:

   ```bash
   module list
   ```

## More module commands with GROMACS as an example

💬 Let's imagine that you want to do some molecular dynamics simulations using the [GROMACS](https://www.gromacs.org/about.html) application.

- It is always a good idea to start by checking [the application list in Docs CSC](https://docs.csc.fi/apps/) to see whether this application is installed in Roihu and how to use it.

1. Check out the [GROMACS page](https://docs.csc.fi/apps/gromacs/).
2. Skim through the documentation and verify that the license allows you to use the software.
3. Check what is the module command that you need to run to be able to load Gromacs in Roihu.
4. Back on the command-line, check which GROMACS versions are available in Roihu.

   ```bash
   module spider gromacs
   ```

   ☝🏻 This might take a while as the command searches through all the available modules.

   💬 The list can be quite long. You can go to the next line with Enter, or stop viewing by typing `q`).

5. Check if some versions can be loaded directly, *i.e.* are compatible with your currently loaded module environment:

   ```bash
   module avail gromacs
   ```

   💡 Tip: Another quick way to list the available versions is by typing the load command until the module name and then hit `TAB` twice:

   ```bash
   $ module load gromacs # and here double press TAB
   gromacs                gromacs/2022.3         gromacs-env/2021-gpu
   gromacs/2021.4-plumed  gromacs/2022.4         gromacs-env/2022
   gromacs/2021.5         gromacs-env            gromacs-env/2022-gpu
   gromacs/2021.6         gromacs-env/2020       
   gromacs/2022.2         gromacs-env/2021
   ```

6. Which version is loaded with the default command? Is it the newest version? Try:

   ```bash
   module load gromacs
   ```

7. Do you notice any changes in the output of `module list` compared to the first try? Try this again:

   ```bash
   module list
   ```  

   ☝🏻 If no version is given in the module command, the default version is loaded.

   - The default version is typically the latest **stable** version of the program.
   - It is recommended to also provide the version in the module load command, as the default version may change.

8. Let's try loading the 2021.6 version specifically:

   ```bash
   module load gromacs/2021.6
   module list
   ```

9. If you want to do something else in the same session, it is usually best to reset the module environment to the default settings. This can be done by first removing all loaded modules and then loading the default environment:

   ```bash
   module purge            # Purge all (non-sticky) modules
   module list             # List the loaded modules
   module load StdEnv      # Load the default module environment
   module list             # List the loaded modules
   ```

## More information

💭 If actually using Gromacs in Puhti, you would run the application as a batch job through the queueing system, which will be discussed in detail later.

💭 Check out an [example batch job script for Gromacs](https://docs.csc.fi/apps/gromacs/#puhti) to see how the module is recommended to be loaded (`module load gromacs-env` loads the latest minor release of a specific year).

### Loading an older version of a module

💬 Using an older version of a module is usually possible

💬 As an example, you can try to load an old version of Gromacs from 2020.

1. The `gromacs/2020.5` module cannot be loaded in the default environment since it has different dependencies. Check with the `module spider` command which other modules are needed for the older version:

   ```bash
   module spider gromacs/2020.5
   ```

2. Load all of the required modules manually before loading `gromacs/2020.5`

   ```bash
   module purge
   module load gcc/9.4.0
   module load openmpi/4.1.4
   module load gromacs/2020.5
   module list
   ```

☝🏻 It is generally best to use the latest versions since they typically are more performant than old ones and may have useful new features.
