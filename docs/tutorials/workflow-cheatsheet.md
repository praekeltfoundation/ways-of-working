# Workflow Cheatsheet

## Setting Up Your Repo

Find the repo you want, get the SSH code

```
$ git clone <git@github:something>
$ cd <REPO>
$ git checkout master
$ git checkout develop
$ git flow init
```

You'll be asked to set some settings. Accept the defaults (hit "Enter" key until it stops doing stuff). So it should look like this:

```
$ Branch name for production releases: [master]
$ Branch name for "next release" development: [develop]
$ Feature branches? [feature/]
$ Release branches? [release/]
$ Hotfix branches? [hotfix/]
```

The first time you enter the repo, you need to pip install some stuff.

```
$ virtualenv ve
$ source ve/bin/activate
(ve)$ pip install <something - check the readme file>
```

For the unicore repos, the pip install commands are like so:

```
(ve)$ pip install -r requirements.txt
(ve)$ pip install -r requirements-dev.txt
```

You're set up :)

## Using the repo
every time you enter your repo

```
$ source ve/bin/activate
```

## Creating a New Feature Branch
Make sure your repo is up to date

```
git checkout develop
git pull
```

Create or find the relevant issue, get the issue number:

```
$ git flow feature start issue-<ISSUE NUMBER>-<BRIEF DESCRIPTION, SEPARATED BY DASH "-" >
$ git branch (just to check which branch you are on)
$ git flow feature publish issue-<ISSUE NUMBER>-<BRIEF DESCRIPTION, SEPARATED BY DASH "-" >
```

## Creating a Pull Request
Make sure the relevant issue has been created within the repository, get the issue number that has been assigned and then:

```
(ve)$ git push
(ve)$ hub pull-request -b develop -i <ISSUE NUMBER>
```

## Checking what other branches exist
This will show local and remote branches. Remote branches (branches on Github) begin with `origin`.

```
git branch -a
```

## Merging a Branch
Make sure you've gotten a +1 or thumbs up in your pull request

```
(ve)$ git checkout develop
(ve)$ git pull
(ve)$ git checkout feature/<BRANCH NAME>
(ve)$ git pull origin develop
(ve)$ git flow feature finish <BRANCH NAME>
(ve)$ git push
```

## Create a release
Check that you're on the develop branch

```
$ git pull
$ git checkout master
$ git pull
$ git checkout develop
$ git flow release start <NEW-VERSION-NUMBER>
```

You will now be on branch `release/<NEW-VERSION-NUMBER>`
You then need to update the version number in the VERSION file using a text editor and then update the CHANGES.rst file, stating what has changed in the update.

```
$ git flow release finish <NEW-VERSION-NUMBER>
```

You will now be back on the develop branch

```
$ git push --tags
$ git push
$ git checkout master
$ git push
$ git checkout develop
```

## Check your branch merge settings and details
Navigate to root of the repo

```
cd .git
nano config
```

Use whatever text editor you want, not nec `nano` to open `config`

## To Delete a Local Branch

```
git branch -d <LOCAL BRANCH NAME>
```


## To revert a commit
Navigate to the repo

```
git log
```

This will display you your last commits and their messages
Find the uuid for the commit you want to undo

```
git revert <UUID>
```

Git will reverse the commit you made and apply that as a new commit

```
git push
```

and my personal favorite, but only to be used when you have messed up beyond comprehension . . .

## When Things Have Gone Terribly Wrong

```
rm -rf <REPO NAME>
```

Then start again . . .
