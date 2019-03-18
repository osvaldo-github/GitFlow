# GitFlow
Test Git Flow

--------------------------------------------------------------------------------------------------------
                                        Git Flow
--------------------------------------------------------------------------------------------------------

Utilizando o fluxo Git Flow
https://medium.com/trainingcenter/utilizando-o-fluxo-git-flow-e63d5e0d5e04

Base de apoio
https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html

Mais informações
https://br.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow

Git Commit Best Practices
https://github.com/trein/dev-best-practices/wiki/Git-Commit-Best-Practices

KDiff3
https://sourceforge.net/projects/kdiff3/

Git Extensions
https://sourceforge.net/projects/gitextensions/


Git Doucmentation
https://git-scm.com/docs


Git Behind A Proxy Server
https://www.freecodecamp.org/forum/t/git-behind-a-proxy-server/13187

git config --global http.proxy http://<username>:<password>@<proxy-server-url>:<port>




-> Pull Requests

About pull requests - READ
https://help.github.com/en/articles/about-pull-requests

About pull request reviews - READ
https://help.github.com/en/articles/about-pull-request-reviews

Reviewing proposed changes in a pull request - READ
https://help.github.com/en/articles/reviewing-proposed-changes-in-a-pull-request

About code owners - READ
https://help.github.com/en/articles/about-code-owners

About pull request merges - Squash - READ
https://help.github.com/en/articles/about-pull-request-merges

Creating a pull request - READ - INTERESTING
https://help.github.com/en/articles/creating-a-pull-request

Requesting a pull request review - READ - INTERESTING
https://help.github.com/en/articles/requesting-a-pull-request-review

Viewing deployment activity for your repository - READ
https://help.github.com/en/articles/viewing-deployment-activity-for-your-repository

Closing issues using keywords - READ
https://help.github.com/en/articles/closing-issues-using-keywords


--------------------------------------------------------------------------------------------------------

\_git
	\master

// Create repository on git remote tool "TestGitFlow"
// Clone into master directory

// Create files

\_git
	\master\TestGitFlow\controllers\controller1.txt
	\master\TestGitFlow\controllers\controller2.txt
	\master\TestGitFlow\controllers\controller3.txt
	\master\TestGitFlow\models\model1.txt
	\master\TestGitFlow\models\model2.txt
	\master\TestGitFlow\models\model3.txt
	\master\TestGitFlow\views\view1.txt
	\master\TestGitFlow\views\view2.txt
	\master\TestGitFlow\views\view3.txt

// Add files	
git add *

// Commit files
git commit -m "Commit controllers, models and views"

// Send changes to the master branch of your remote repository
git push origin master


[SITE]
// List all local and remote branchs
git branch -a

--------- result ---------
* master
  remotes/orign/master
--------------------------

// List the files you've changed and those you still need to add or commit
git status

// Switch from one branch to another
git checkout <branchname>

// List local branchs
git branch

// To drop all your local changes and commits, fetch the latest history 
// from the server and point your local master branch at it, do this
git fetch origin

// Create a new branch and switch to it
git checkout -b <branchname>

// Push the branch to your remote repository, so others can use it
git push origin <branchname>

[SITE]
// Sync remote repository && Create branch (with all files from origin) and swith to it && Push branch to remote repository
git fetch origin && git checkout -b develop && git push origin develop

-> Verify in your remote repository tool that new branch is created with files.



**********************************
feature: para novas implementações

release: para finalizar o release e tags

hotfix: para resolver problema crítico em produção que não pode esperar novo release
**********************************

// Show all local branch and how is selected (*)
git branch

--------- result ---------
* develop
  master
--------------------------

// Already be in develop branch, otherwise
git checkout develop



<<< FEATURE/NOVO-COMPONENTE BRANCH >>>



[SITE]
// Create new 'feature' branch.
// Remember: this operation copy all files from orign (origin is set now with develop branch)
git checkout -b feature/novo-componente

[SITE]
// push to remote repository
git push origin feature/novo-componente

// Create directories and clone correct branch

\_git
	\develop\TestGitFlow\...
	\feature\novo-componente\TestGitFlow\...
	
	
// Navigate to directory
_git\feature\novo-componente\TestGitFlow\
	
// And create a file
document1.txt

// Select branch, add file, commit and push
git checkout feature/novo-componente
git add *
git commit -m "Commit document1 from feature/novo-componente branch"
git push origin feature/novo-componente

[SITE]
// Select develop repository && Perform local merge between two branchs && Push updates to develop remote branch
git checkout develop && git merge feature/novo-componente && git push origin develop



<<< RELEASE BRANCH >>>

[SITE]
// Create branch release/v1.0.1 && Push to remote repository
git checkout -b release/v1.0.1 && git push origin release/v1.0.1


<<< TAG >>>

[SITE]
// Create a tag
git tag -a v1.0.1 -m "Release do novo componente"

[SITE]
// Show and push
git show v1.0.1 && git push origin v1.0.1


<<< MASTER BRANCH >>>


// Select master repository && Merge 
git checkout master && git merge release/v1.0.1               -----> I couldn't execute this. Tortoise tool was necessary.
                                                                     VERIFY: Tortoise use Fast-Forward

// Push to remote repository
git push origin master


// Navigate to directory
_git\master\TestGitFlow\

// Fetch and merge changes on the remote server to your working directory
git pull



--------------------------------------------------------------------------------------------------------
                                BEST PRACTICES
--------------------------------------------------------------------------------------------------------


1. Always use Fetch before Pull.

What is the difference between 'git pull' and 'git fetch'?
https://stackoverflow.com/questions/292357/what-is-the-difference-between-git-pull-and-git-fetch
In the simplest terms, git pull does a git fetch followed by a git merge.

Example: 

In branch develop:

NEW DOCUMENT

a - create document2.txt (remote repository)
b - open develop workspace directory
c - $ git checkout develop
d - $ git fetch (download document2.txt from remote to local repository)
e - $ git diff origin/develop (see all differences between workspace and local repository)
f - $ git merge (download document2.txt from local repostory to workspace)
g - verify your workspace directory

ALTER DOCUMENT

a - alter document2.txt (remote repository)
b - open develop workspace directory
c - $ git checkout develop
d - $ git fetch (download document2.txt changes from remote to local repository)
e - $ git diff origin/develop (now you see differences between workspace and local repository)
f - alter again document2.txt (remote repository)
g - $ git fetch (download document2.txt changes from remote to local repository)



Saving Changes with Git Stash
https://mijingo.com/blog/saving-changes-with-git-stash

git stash list
stash save "updated the offline file"
git stash pop 
git stash pop stash@{0}
git stash apply
git stash apply stash@{0}
git stash list
git stah drop
git stah drop stash@{0}
git stash --help


2. Overview Structure

- Git is separeted into 4 layers:
  working_dir || staging_area (index) || local_repo || remote_repo

git diff -> differences between work directory and staging
git diff origin/develop -> differences between work directory and local repository


-> Change Remote and Change Local

1. altered document3.txt in remote
2. altered document3.txt in local
3. 'git diff' and git 'diff origin/develop' are same result, only appear local changes
4. 'git fetch' download chages from remote_repo to local_repo
5. 'git diff' continues appear local changes and now 'git diff origin/develop' appear remote changes
6. Now you can´t perform commit or merge.
7. Save on stash 'git stash save 'document3.txt at 15:24'', now working_dir is empty changes
8. Perform 'git merge', now working_dir contains only remote changes
9. Apply stash 'git stash apply stash@{0}'
10.Conflit files is showed. To resolve this uses a tool diff.
11.Use mine text block then theirs


--------------------------------------------------------------------------------------------------------


How to Use Git Merge [the Correct Way]
https://dev.to/neshaz/how-to-use-git-merge-the-correctway-25pd

[Git] Entendendo as Estratégias de Merge Fast-Forward e Three-Way
https://medium.com/@andgomes/git-entendendo-as-estrat%C3%A9gias-de-merge-fast-forward-e-three-way-8eff92fca086

How to delete a remote tag?
https://stackoverflow.com/questions/5480258/how-to-delete-a-remote-tag

// Delete remote tag
git push --delete origin tagname

// Delete local tag
git tag --delete tagname



--------------------------------------------------------------------------------------------------------
                            Resolving Merge Conflict - Pull Request
--------------------------------------------------------------------------------------------------------


Checkout via command line
If you cannot merge a pull request automatically here, you have the option of checking it out via command line to resolve conflicts and perform a manual merge.

HTTPS
Git
Patch
https://github.com/osvaldo-github/GitFlow.git
Step 1: From your project repository, bring in the changes and test.

git fetch origin
git checkout -b FlyDogBR-patch-2 origin/FlyDogBR-patch-2
git merge develop
Step 2: Merge the changes and update on GitHub.

git checkout develop
git merge --no-ff FlyDogBR-patch-2
git push origin develop



--------------------------------------------------------------------------------------------------------
                                        Katacoda
--------------------------------------------------------------------------------------------------------





Scenario 1 - Commiting Files

git init
git status
git add hello-world.js
git status
git commit -m "Initial Hello World Commit"
echo '.*tmp' > .gitignore
git add .gitignore
git commit -m "gitignore file"


Scenario 2 - Commiting Changes

gi status
git diff
git diff <hash commit>
git difftool
git add
git mv
git rm

//this
git mv oldname newname
//is just shorthand for:
mv oldname newname
git add newname
git rm oldname



--------------------------------------------------------------------------------------------------------