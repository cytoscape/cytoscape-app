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
* Go into the app's directory.  Let's use ___smbl___ as an example.

```
cd sbml
```

* Check the status of sbml app directory:

```
~/p/c/a/sbml git:master ❯❯❯ git status
HEAD detached at 947e5ca
nothing to commit, working directory clean
```



