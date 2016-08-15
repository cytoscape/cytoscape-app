# Cytoscape Core Apps

This is the top-level maven project for all Core Apps.

## How to build

```
git clone git@github.com:cytoscape/cytoscape-app.git
cd cytoscape-app
git submodule init
git submodule update
mvn clean install
```

## Working with Core Apps
Each core app has its own GitHub repository.  You can work on those as if you are working on a completely independent app project.  However, since they are totally independent from any of the core modules, you need to be careful when you want to reflect your changes to the core.

### Submodules
If you are not familier with git submodules, please read the following documents to understand basic concepts:

* [7.11 Git Tools - Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)  
* [Git command reference: git-submodule - Initialize, update or inspect submodules](http://git-scm.com/docs/git-submodule)

Don't be scared!  The only thing you need to understand is, ___a submodule is a pointer to particular commit___.  That's all.  You can try ```git submodule status``` command to see this is true:

```bash
~/p/c/app git:develop ❯❯❯ git submodule status
 e59d6ecd0a18edb3752753da5351d84bca8988a9 biopax (3.3.0-coreapp-init)
 9a76965cc257b35d2a7954a0d490c58894b1eb6d command-dialog (3.3.0-coreapp-init)
 04a53e651f6e3789a16620c1d639192db8b57ca9 cyREST (1.1.1-11-g04a53e6)
 15e2994de7a619977fb07b422ec5b0ea998c52f1 datasource-biogrid (3.3.0-coreapp-init)
 37e37e02e72e27a2ff5a086efff373ad4a3ff374 network-analyzer (3.3.0-coreapp-init-2-g37e37e0)
 a68a99fbedb7c19e88f1758792a7e9a2816e61ec network-merge (3.3.0-coreapp-init-2-ga68a99f)
 8f629dcf4ba0d86a369abce815d250c4cddcfe2e psi-mi (3.3.0-coreapp-init-1-g8f629dc)
 947e5ca1d8ff2fda6f41852687073369b52ca574 sbml (3.3.0-coreapp-init)
 78e6e424115f45ea5f6ddfe1bef2e7fc6b176ab1 webservice-biomart-client (3.3.0-coreapp-init)
 c67b8bd366b107634529585974406b5161e47c22 webservice-psicquic-client (3.3.0-coreapp-init)
 7ed0e24c5e4d16d2442e899a25ee936733e01ca5 welcome (3.3.0-coreapp-init-2-g7ed0e24)
```

All Core Apps in this directory are just pointers to specific commits (left).

## Workflow Example: Developing new feature for SBML reader
In this section, you will learn how to refrect your changes in an app to the core.


### Synchronize an App Project
First of all, let's go into one of the apps' directory.  We will use ___smbl___ as an example.

```
cd sbml
```

#### Check the status of sbml app directory:

```
~/p/c/a/sbml git:master ❯❯❯ git status
HEAD detached at 947e5ca
nothing to commit, working directory clean
```

Now you can see this is __NOT__ a regular branch.  It is called ___detached HEAD___ which is an ophan isolated from all branches.  Remember, since submodule is a pointer to a commit (associated with a hash), this is normal.


#### Move to a regular branch
To go back to a regular branche, in our case ___master___, type the following command:

```
git checkout master
```

and check the status again.

```
/p/c/a/sbml git:master ❯❯❯ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
```

Now you are ready to write your code.  We will use [GitHub Flow](https://guides.github.com/introduction/flow/) model for all core apps, and the first thing you need to do is create a new feature branch.  Give a descriptive name for your new feature branch:

```
git checkout -b update-readme
```

#### Commit new changes
Once you finish your work, just follow the regular workflow:

```git
~/p/c/a/sbml git:update-readme ❯❯❯ git status                                                                                                                   ✱
On branch update-readme
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

~/p/c/a/sbml git:update-readme ❯❯❯ git add -A                                                                                                                   ✱
~/p/c/a/sbml git:update-readme ❯❯❯ git commit -m "README updated for SBML Reader App."                                                                          ✚
[update-readme 316ed8d] README updated for SBML Reader App.
 1 file changed, 6 insertions(+)
~/p/c/a/sbml git:update-readme ❯❯❯ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.

~/p/c/a/sbml git:master ❯❯❯ git merge update-readme
Updating 9ec0874..316ed8d
Fast-forward
 README.md | 6 ++++++
 1 file changed, 6 insertions(+)
~/p/c/a/sbml git:master ❯❯❯ git push
```

You can repeat this cycle, ___branch-->code-->commit-->merge___, as many times as you want.

#### Reflect changes to the core
At this point, you worked only on the SBML reader repository.  Even if you create a lot of new features in apps, core does not know anything about those.  Once you are ready to publish those new features to other core developers, you need to update the pointer in the ___app___ directory to the latest commit you made for the SBML reader.  This is REALLY simple:


```
cd ..
git status                                                                                                                            ✱
On branch develop
Your branch is up-to-date with 'origin/develop'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   sbml (new commits)

no changes added to commit (use "git add" and/or "git commit -a")
```

You can see that new commits are available for the sbml reader directory.  Let's commit the change to the core:

```
~/p/c/app git:develop ❯❯❯ git add -A                                                                                                                            ✱
~/p/c/app git:develop ❯❯❯ git status                                                                                                                            ✚
On branch develop
Your branch is up-to-date with 'origin/develop'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   sbml

~/p/c/app git:develop ❯❯❯ git commit -m "README updated for SBML Reader App."                                                                                   ✚
[develop a0631d5] README updated for SBML Reader App.
 1 file changed, 1 insertion(+), 1 deletion(-)
~/p/c/app git:develop ❯❯❯ git push                                                                                                                              ⬆
warning: push.default is unset; its implicit value has changed in
Git 2.0 from 'matching' to 'simple'. To squelch this message
and maintain the traditional behavior, use:

  git config --global push.default matching

To squelch this message and adopt the new behavior now, use:

  git config --global push.default simple

When push.default is set to 'matching', git will push local branches
to the remote branches that already exist with the same name.

Since Git 2.0, Git defaults to the more conservative 'simple'
behavior, which only pushes the current branch to the corresponding
remote branch that 'git pull' uses to update the current branch.

See 'git help config' and search for 'push.default' for further information.
(the 'simple' mode was introduced in Git 1.7.11. Use the similar mode
'current' instead of 'simple' if you sometimes use older versions of Git)

Counting objects: 2, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 273 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
To git@github.com:cytoscape/cytoscape-app.git
   731bc31..a0631d5  develop -> develop
```

That's it!

## Best Practices

* When you work on Core Apps, work only on the repository until you finish a task (new features or bug fixes)
* Once you reach to a major milestone, go back to ___app___ directory and update the submodule





