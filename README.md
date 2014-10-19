# How to Merge Code

## Table of Contents

* [Purpose](#purpose)
* [Detailed Steps](#detailed-steps)
* [Additional Reading](#additional-reading)

## <a name="purpose"></a>Purpose
This guide explains how to develop and commit your code using git and GitHub. A developer should create a feature branch when developing new code. In the feature branch, a developer may commit multiple times during development including making changes based on comments from a code review. When development is completed and the feature branch is ready to be merged in to the master branch, the developer should squash the commits in to one, so that the git log history is kept clean. 

## <a name="detailed-steps"></a>Detailed Steps
1. On the `master` branch, `git pull` to make sure your code is up to date.
2. Create a feature branch `git checkout -b name-of-feature-branch`. Note, you will automatically be switched to this new feature branch you are creating.
3. Write code and develop your feature.
4. `git commit` your code. Note, this step may be performed as many times as you prefer during development in order to maintain a history of your code changes.
5. Once development is completed (and all your code is committed), we should make sure that our code is up to date with the latest `master` branch. On your feature branch, `git rebase master` will ensure that your branch is up to date and your code is compatible with the latest `master`. Also this step ensures that your commits are at the top, which is critical for the next steps.
Note that, during the rebase, you may encounter merge conflicts that will need to be resolved.
6. Now we need to push our code to GitHub. `git push origin name-of-feature-branch` (while on the name-of-feature-branch branch) to push the branch to GitHub.
7. In GitHub, create a pull request for the name-of-feature-branch branch and assign someone to review your code.
8. If the reviewer makes comments or suggestions, please address them by asking for clarification and/or committing the changes. The reviewer also needs to give approval on whether or not the code is ready to be merged.
9. Once the code is ready to be merged, it is time to squash your commits. Note, this doesn't apply if you only have one commit to merge, and in that case you can just merge your pull request on GitHub. First we need to know at what point your branch and master diverge. This is required as you only want to squash your commits. 
10. To do this run `git merge-base master <mybranch>`.  This command should spit out a commit hash such as _918310dca623fac2d46198324814695c4726017e_. You will then use this hash to tell git  "_squash the commits from this point on_".
9. Once you have your merge base commit run `git rebase -i <commit-hash>`, for example: `git rebase -i 918310dca623fac2d46198324814695c4726017e`. 
10. Your text editor should popup and you should see your commits with the word `pick` in front of them. For all commits except the first one, change `pick` to `squash` or `s`, which will squash all of these commits in to one. Now save and quit your text editor.
11. Another text editor window should pop up now, and here you can enter the commit message you would like to show up. This commit contains all of your commits squashed together.
12. In order for this to work with your existing GitHub pull request (because we are rewriting the git log history), we need to `git push origin name-of-feature-branch -f`, which forces the push to overwrite the git log history in that pull request.
13. You should see that on your GitHub pull request, the history should only contain the one commit that you squashed.
14. Press the Merge button, and don't forget to delete your remote feature branch!

## <a name="additional-reading"></a>Additional Reading
* https://help.github.com/articles/about-git-rebase
* https://help.github.com/articles/using-git-rebase
* http://git-scm.com/book/en/Git-Tools-Rewriting-History
* http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html
