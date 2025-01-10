---
layout: default
title: 1 - Repositories
nav_order: 3
toc: true
last_modified_date: "2024-08-20 02:13AM"
---

# Creating and Managing Git Repositories
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .no_toc .text-delta }
- TOC
{:toc}
</details>

Creating a new repository is often confusing to new users of Git and GitHub. Here is a simple explanation of the two options, with complete instructions on how to work with each.

The `git` command displays these options within the `--help` documentation:

```
start a working area (see also: git help tutorial)
   clone     Clone a repository into a new directory
   init      Create an empty Git repository or reinitialize an existing one
```

{: .warning :}
It is important to remember that when **cloning** or **forking** an existing repository, you will inherit the _entire history_ of all previous commits. This is a feature: Newcomers to a project are not restricted to only the history after their arrival.


## Clone

`git clone` is the simplest way to begin working with a repository you want connected to GitHub. The `clone` operation clones an entire remote repository to your local workstation.

Assuming you are authenticating to GitHub using SSH keys, here are the steps to cloning:

1. Within [GitHub](https://github.com/) find the existing repository you want to clone.
2. From the repository page, find the blue "Code" button, and select the SSH tab within the dropdown. If you are using a PAT for authentication, use the HTTPS address.
3. Copy the address, which will look something like `git@github.com:UVADS/git-basics.git` (SSH) or `https://github.com/UVADS/git-basics.git` (HTTPS). 
4. In the command-line on your local computer, clone the repo. If using an SSH key to authenticate to GitHub, use this format:

    ```
    git clone git@github.com:UVADS/git-basics.git
    ```

    If using a PAT to authenticate to GitHub, be sure to insert your token in the clone command like this:

    ```
    git clone https://ghp_xxxxxxxxxxxxxxx@github.com/UVADS/git-basics.git

5. This will create a new subdirectory with the name of the repository. You can change the name of the directory if you like.
6. If there are multiple branches in the GitHub repository and you want to clone them all, use these commands (using this repository as an example):

    ```
    # Using SSH
    git clone git@github.com:UVADS/git-basics.git
    cd git-basics/
    git fetch --all
    for branch in `git branch -r | grep -v HEAD`; do
      git checkout -b $branch $branch
    done
    ```

    ```
    # Using a PAT
    git clone https://ghp_xxxxxxxxxxxxxxx@github.com/UVADS/git-basics.git
    cd git-basics/
    git fetch --all
    for branch in `git branch -r | grep -v HEAD`; do
      git checkout -b $branch $branch
    done
    ```

7. Note that if you create a new, empty repository within GitHub, it is helpful to tick the box to include a `README.md` file by default. This ensures that a default branch (named `main`) will be created for you.


## Init

Git repositories can also be created locally and connected with GitHub after creation. (In fact, there are some cases where a local git repository is used for source control but never connected to an external hub.) 

To initialize a local `git` repository and then connect it with GitHub:

1. Create a directory for your new project and `cd` into it.
2. Issue the `git init` command to initialize the repository.
3. Then add a file and commit it
4. Create a default branch.

    ```
    mkdir project1
    echo "# foo" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git branch -M main
    ```

4. Next, create an empty repository in GitHub. Do not add a README.md file in that process (leave that unchecked). You will see prompts for how to:
    - Create a new repository from the command line
    - Push an existing repository from the command line (the path followed below)
    - Import code from another repository
5. Copy the SSH URL to your new repository, which will look something like `git@github.com:<account>/<repo>.git`
6. Finally, add the remote origin and push your repo using that URL:

    ```
    git remote add origin git@github.com:<account>/<repo>.git
    git push -u origin main
    ```

## Fork

A fork is a copy of someone else’s repository. This is usually because you do not have access to push changes to the repository, or because the organization that controls it requires all changes come through forks and pull requests.

When you fork a repository, a complete copy is made in your own account (or Organization) in GitHub. This gives you complete control to clone and work with the code freely. You own the forked copy, so you can make additions, new functionality, and commit+push to your own fork.

{: .success :}
[**Learn more about Forks**](docs/forks-branches/)

## Delete

To delete a repository you have both in GitHub and on your local computer, do the following:

1. Locally, `cd ../` to the parent directory above your project directory, and `rm -Rf <project-name>` to delete the entire folder. You can also use the MacOS Finder or Windows Explorer to select and delete this folder.
2. In GitHub, within the repository page itself, click the "Settings" tab, and scroll to the bottom. There you will find a "Delete this repository" button.
