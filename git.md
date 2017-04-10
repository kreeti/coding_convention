# Git

* Write a good commit message with story number(if present).

  ```
  [#102] Update scope for unattach items
  ```

* Remove buffer file during commit your changes.

* Create different branch for different story and Each branch should contain maximum 2 commit messages.

* Create Pull Request only after finish the task competely of a particular story.

* Do not amend your commit if pull request is already created. If there is more than 2 commits , squash them.

* Do not change anything in master branch, always create seperate branch.

* Rebase frequently to incorporate upstream changes.

* If any branch merge with master branch, then delete that branch from local as well as master.

* Before creating Pull Request review code yourself once.

* Use `gitk` to see the changes from local machine

* Do not upload credentials files or any secret file in git, add them in `.gitignore`

* Always create new branch from master.

* Always take pull from master branch before starting your work.

* Use 'git diff' to see what changes you have done.

* To work on different branch which is not your local branch , you have to retrack it. For this go to your master branch then use 'git fetch -p origin'

* Delete unnecessary local branches.