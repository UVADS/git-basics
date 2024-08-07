---
layout: default
title: 0 - Install & Setup
nav_order: 2
---

# Install and Set Up Git

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

Setting up git and authenticating yourself to GitHub is an important first step in managing and tracking your code and various projects. Follow the steps for your platform below

## GUI or Command-Line?

Developers should always feel empowered to select and use the tools they feel most comfortable with. There is no superiority or shame in selecting a GUI over the command-line `git` tool. Generally, most every feature is available in either.

While most data scientists tend to use `git` from the command-line, many use a GUI every day.

Advantanges of using a GUI for `git`:

- Simple to use.
- Handles dragging and dropping of files.
- Visually displays changes, errors, and status.
- Makes resolving merge conflicts much simpler.
- [**GitHub Desktop**](https://github.com/apps/desktop) is an excellent, free choice. There are many other free and paid `git` clients available.

Here is what **GitHub Desktop** looks like:

![GitHub Desktop](https://images.ctfassets.net/8aevphvgewt8/5fErhOtgvjrf97d7wOoARB/b262e06c615977f33046c468147aa114/screenshot-windows-dark.png)

Advantages of using the CLI version of `git`:

- Fastest way to access all commands.
- Displays only what the developer wants to see, allowing for focus.
- Might be the only way to use `git` in a remote system (HPC cluster, cloud instances, etc.)

In order to focus on specific operations and workflow steps using `git` this documentation references CLI commands only. We recommend learning those commands to get the concepts, and then learn how they are done in a GUI.

## Command-Line `git`

Data scientists and software developers who write code regularly *greatly* tend to use the terminal/command-line to interact with `git`. This primer assumes this and does not address various GUI tools for working with `git` and GitHub.

### Mac

**Here's a walkthrough for Mac users on how to set up git, SSH keys, and GitHub.**

[![Install SSH Keys in Git using a Mac](https://i.ytimg.com/vi/rajlGZ3w4OU/maxresdefault.jpg)](https://www.youtube.com/embed/rajlGZ3w4OU?si=UPknm4ygzhenNrRN)

<ol style="list-style-type: decimal;">
    <li>Install Git using the instructions at the following link. A git GUI version is optional, but the command line version is required for this course: <a href="https://git-scm.com/book/en/v2/Getting-Started-Installing-Git" target="_blank" rel="noopener">https://git-scm.com/book/en/v2/Getting-Started-Installing-Git</a>&nbsp;</li>
    <li>Check that git is installed in your environment by issuing the <code>git</code> command.</li>
    <li>Sign into GitHub by following the instructions for SSH key authentication. (Note that username/password authentication will NOT work using the command line.) The <code>ssh-keygen</code> tool is available to MacOS, Linux, and <code>git-bash</code> (Windows) users. <a href="https://docs.github.com/en/get-started/quickstart/set-up-git" target="_blank" rel="noopener">https://docs.github.com/en/get-started/quickstart/set-up-git</a>&nbsp;</li>
    <li>See the screencast above for a walkthrough.</li>
</ol>


### Windows

**Here's a walkthrough for Windows users on how to set up git-bash, SSH keys, and GitHub.**

[![Install SSH Keys in Git using a Mac](https://i.ytimg.com/vi/X2JgmpkahrY/maxresdefault.jpg)](https://www.youtube.com/embed/X2JgmpkahrY?si=TTvzELmRHoT2jJpM)

Using `ssh-keygen.exe` in `git-bash` creates a keypair successfully, but (apparently) permissions are incorrect and the normal `chmod 700 keyname` on the private key does not work. This means that git cannot authenticate to GitHub. To resolve this:

<ol style="list-style-type: decimal;">
    <li>Use the <code>ssh-keygen.exe</code> command in git-bash to create a new keypair. Use all the default settings; you do not need to set a password for your key.</li>
    <li>In Windows Explorer, open your <code>.ssh</code> directory and right-click your <code>id_rsa</code> private key. (It may have more numbers and letters added to the name - that's okay.) An easy way to open Windows Explorer in your current directory is: <code>explorer .</code></li>
    <li>Select Properties, then the Security tab and click Edit...</li>
    <li>Check the Deny box next to "Full Control" for all groups EXCEPT Administrators. In my test I only needed to "Deny" full control to the SYSTEM group.</li>
    <li>If you have not already, cat out and copy the contents of your <code>id_rsaXXXX.pub</code> public key to your clipboard. Then visit <a href="https://github.com/settings/keys" target="_blank" rel="noopener">https://github.com/settings/keys </a>and add a New SSH Key. You can name it something convenient and then paste the public key into the "Key" field and save.</li>
    <li>Retry your <code>git</code> commands. You will know it works correctly when you can modify a file, git add it, git commit it, and then git push your changes back to GitHub.</li>
    <li>See the screencast above for a walkthrough.</li>
</ol>

### Linux

Install `git` in a Linux distro with the built-in package manager:

Ubuntu:

    sudo apt update && apt install git

CentOS/RHEL:

    sudo yum install git

Then set up your authentication method (SSH keys or PAT) and configure as instructed below.

## Authentication Options

GitHub offers two ways to authenticate your local workstation with GitHub. Usernames and passwords are no longer an option,
as they present security risks. Instead use one of these:

- **SSH Keys** - the above walkthroughs used SSH keypairs to authenticate your computer to GitHub. These allow your pushes and pulls, etc. to authenticate seamlessly to GitHub as a full owner of the repository.
- **Personal Access Tokens (PATs)** - PATs are long, randomized tokens that can be scoped with specific levels of permissions. More on how to authenticate using PATs [can be found here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).

## First-time Configuration

Confirm your installation is working by issuing the `git` command from within your terminal. You should see a number of subcommands avaialable to you.

The first time you use git you will encounter a couple of setup issues:

- The first time you clone a repository from GitHub using a new ssh key you will get a "key fingerprint" approval request. You can safely say "Yes" to this request, which you will only be asked once.
- The first time you try to commit code on your laptop using `git` you will be asked to configure two global settings - your name and email. These settings identify you in the log of commits and changes. Here are the two settings; replace the values in quotes with your own info:


        git config --global user.name "Your Name"
        git config --global user.email "mst3k@virginia.edu
