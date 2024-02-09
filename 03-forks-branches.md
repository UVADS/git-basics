# Branches Forks & Merges

Git enables software developers to copy an existing codebase and work with the copy alongside the original, without one interfering with the other. 

- The easiest way to copy your entire project code and work with it is called a "Branch".
- The method for copying someone else's project in order to work with is called a "Fork".
- Bringing your changes back into either your project or someone else's is called a "Merge". This function is called a "Pull Request" in GitHub.

## Branches

The default branch of most repositories is called `main`. Many developers do their everyday work adding and committing to the `main` branch. But what if you would like to experiment with a new library, or test out new functionality without disrupting the functionality of the original code? This is what a branch is for.

A new branch is a complete copy of your code that can have an independent life from the branch it was copied from. 

To create a new branch (based on a copy of the branch you are currently using)
```
git branch development
```
To work with the new branch:
```
git checkout development
```
To list all your branches, and indicate which you are currently on (denoted by the `*`)
```
$ git branch
  dev
* main
```

Branches generally end up in one of two possible states:

- The idea / experiment / feature / test that motivated creating the branch in the first place is abandoned and the branch can be deleted. Perhaps the test was unsatisfactory in some way, or impossible to deliver, or otherwise deemed unsuccessful. See [how to delete a branch](#deleting-a-branch) below.
- The new functionality of the branch is considered successful, and you want to fold the new code into the original branch. See [merges & pull requests](merges--pull-requests) below.

### Deleting a branch

To delete a branch:
```
git branch -d <branch-name>
```

## Forks

## Merges / Pull Requests