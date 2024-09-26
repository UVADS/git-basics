---
layout: default
title: 0 - Install & Setup
nav_order: 2
last_modified_date: "2024-08-25 02:13AM"
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

### Installation

[Download git]([docs/setup/](https://git-scm.com/downloads)){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

<ol style="list-style-type: decimal;">
    <li>Install Git using the instructions at the following link. A git GUI version is optional, but the command line version is recommended: <a href="https://git-scm.com/book/en/v2/Getting-Started-Installing-Git" target="_blank" rel="noopener">https://git-scm.com/book/en/v2/Getting-Started-Installing-Git</a>&nbsp;</li>
    <li>Check that the `git` CLI is installed in your environment by issuing the <code>git</code> command.</li>
</ol>

## First-time Configuration

Confirm your installation is working by issuing the `git` command from within your terminal. You should see a number of subcommands avaialable to you.

The first time you use git you will encounter a couple of setup issues:

- The first time you clone a repository from GitHub using a new ssh key you will get a "key fingerprint" approval request. You can safely say "Yes" to this request, which you will only be asked once.
- The first time you try to commit code on your laptop using `git` you will be asked to configure two global settings - your name and email. These settings identify you in the log of commits and changes. Here are the two settings; replace the values in quotes with your own info:


      git config --global user.name "Your Name"
      git config --global user.email "mst3k@virginia.edu

## Signing In

GitHub offers two ways to authenticate your local computer to GitHub. Usernames and passwords are no longer an option, as they present security risks. Instead you can use SSH keys or Tokens. We recommend you use a token.

- **Personal Access Tokens (PATs)** - PATs are long, randomized tokens that can be scoped with specific levels of permissions. More on how to authenticate using PATs [can be found here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens). More details about how to configure your local system [are also available](../token-authentication). Or watch the video below:

    [Learn about Tokens](../token-authentication/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

    To clone a repository authenticated using a token, the command and URL of the repository will look something like:

    ```
    git clone https://github.com/ACCOUNT/REPOSITORY.git
    ```

    [![Using a Personal Access Token with GitHub](https://i.ytimg.com/vi/C4R2mMx6C-k/maxresdefault.jpg)](https://www.youtube.com/embed/C4R2mMx6C-k?si=UPknm4ygzhenNrRN)

- **SSH Keys** - you can also use SSH keypairs to authenticate your command-line to GitHub. These allow your pushes and pulls, etc. to authenticate seamlessly to GitHub as a full owner of the repository. More about SSH authentication to GitHub is [available here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

    [Learn about SSH](../ssh-authentication/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

    To clone a repository authenticated using SSH keys, the command and URL of the repository will look something like:

    ```
    git clone git@github.com:ACCOUNT/REPOSITORY.git
    ```

    [![Using SSH keys with GitHub](https://i.ytimg.com/vi/rajlGZ3w4OU/maxresdefault.jpg)](https://www.youtube.com/watch?v=rajlGZ3w4OU)

## Troubleshooting Authentication

- SSH key warnings are verbose and should be somewhat easy to interpret.

- When a PAT is invalid, the user will be given a `username` and `password` prompt. This is likely because the PAT has expired or is malformed.
  
- Remember that if you inject your PAT token value into the GitHub repository URL in the moment of cloning, that token is hard-coded into the `.git/config` file of that repository. You should [update that URL](https://uvads.github.io/git-basics/docs/git-advanced/#change-from-ssh-to-token-authentication) with a fresh PAT as needed.

## Key Rotation

Whether you use SSH keys or PATs to authenticate to GitHub or any other provider, it is highly recommended
that you rotate them at least once a year. This ensures that a stolen or shared key, that is still active,
does not offer an attacker any privileges to your account.

### To remove an SSH key from GitHub

1. Go to https://github.com/settings/ssh
2. Find the public key you want to remove.
3. Use the "Delete" button to remove it from GitHub.
4. Delete the corresponding private key on your local computer.

### To remove a PAT from GitHub

1. Go to https://github.com/settings/tokens
2. Find the token you want to remove.
3. Use the "Delete" button to remove it from GitHub.
