# Creating and Managing Git Repositories

Creating a new repository is often confusing to new users of Git and GitHub. Here is a simple explanation of the two options, with complete instructions on how to work with each.

The `git` command displays these options within the `--help` documentation:

```
start a working area (see also: git help tutorial)
   clone     Clone a repository into a new directory
   init      Create an empty Git repository or reinitialize an existing one
```

## Clone

`git clone` is the simplest way to begin working with a repository you want connected to GitHub. The `clone` operation clones an entire remote repository to your local workstation.

Assuming you are authenticating to GitHub using SSH keys, here are the steps to cloning:

1. Within [GitHub](https://github.com/) find the existing repository you want to clone.
2. From the repository page, find the blue "Code" button, and select the SSH tab within the dropdown. If you are using a PAT for authentication, use the HTTPS address.
3. Copy the address, which will look something like `git@github.com:UVADS/git-basics.git` (SSH) or `https://github.com/UVADS/git-basics.git` (HTTPS). 
4. In the command-line on your local computer, clone the repo:

```
git clone git@github.com:UVADS/git-basics.git
```

5. This will create a new subdirectory with the name of the repository. You can change the name of the directory if you like.
6. If there are multiple branches in the GitHub repository and you want to clone them all, use these commands:

```
git clone git@github.com:UVADS/git-basics.git
cd <repository-name>
git fetch --all
for branch in `git branch -r | grep -v HEAD`; do
  git checkout -b $branch $branch
done
```

7. Note that if you create a new, empty repository within GitHub, it is helpful to tick the box to include a `README.md` file by default. This ensures that a default branch (named `main`) will be created for you.

## Init

Git repositories can also be created locally and connected with GitHub after creation. (In fact, there are some cases where a local git repository is used for source control but never connected to an external hub.) 

To initialize a local git repository and then connect it with GitHub:

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

4. Next, create an empty repository in GitHub. Do not add a README.md file in that process (leave that unchecked).
5. Copy the SSH URL to your new repository, which will look something like `git@github.com:<account>/<repo>.git`
6. Finally, add the remote origin and push your repo.

```
git remote add origin git@github.com:<account>/<repo>.git
git push -u origin main
```
