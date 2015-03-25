Git Protocol
============

A guide for programming within version control.

Maintain a Repo
---------------

* Avoid including files in source control that are specific to your
  development machine or process.
* Delete local and remote feature branches after merging.
* Perform work in a feature branch.
* Rebase frequently to incorporate upstream changes.
* Use a [pull request] for code reviews.

[pull request]: https://help.github.com/articles/using-pull-requests/

Write a Feature
---------------

Naming your branch

* There is a story id (click the 'ID' box next to it.).  This is the first of the three parts.
* There is a description.  This is the second part.
* We define work as either a feature, a bug or a chore.  This is the third part.
* These part are separated with a forward slash '/'

	- 87654321/this-changes-everying/feature
	- 87654321/this-fixes-everying/bug
	- 87654321/this-makes-everying-better/chore

Create a local feature branch based off master.

    git checkout master
    git pull
    git checkout -b <branch-name>

<!--Prefix the branch name with your initials.
-->
Share your branch.

    git push origin <branch-name>



Rebase frequently to incorporate upstream changes.

    git fetch origin
    git rebase origin/master

Resolve conflicts. When feature is complete and tests pass, stage the changes.

    git add --all

When you've staged the changes, commit them.

    git status
    git commit --verbose

Write a [GOOD COMMIT MESSAGE] please. Example format:

    Present-tense, active-voice summary under 50 characters [ID#]

    * More information about commit (under 72 characters).
    * More information about commit (under 72 characters).

    https://www.pivotaltracker.com/n/projects/123456/stories/12345678

If you've created more than one commit, use a rebase to squash them into
cohesive commits with good messages:

    git rebase -i origin/master

Submit a [GitHub pull request].

Ask for a code review in the project's chat room.

[good commit message]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
[GitHub pull request]: https://help.github.com/articles/using-pull-requests/


STOP READING HERE
-----------
WIP Commits
-----------

At the end of a hard day, we should always push code to the cloud.

    git checkout <branch-name>
    ./bin/setup
    git diff staging/master..HEAD


Review Code
-----------

A team member other than the author reviews the pull request. They follow
[Code Review](/code-review) guidelines to avoid
miscommunication.

They make comments and ask questions directly on lines of code in the GitHub
web interface or in the project's chat room.

For changes which they can make themselves, they check out the branch.

    git checkout <branch-name>
    ./bin/setup
    git diff staging/master..HEAD

They make small changes right in the branch, test the feature on their machine,
run tests, commit, and push.

When satisfied, they comment on the pull request `Ready to merge.`

Merge
-----

Rebase interactively. Squash commits like "Fix whitespace" into one or a
small number of valuable commit(s). Edit commit messages to reveal intent. Run
tests.

    git fetch origin
    git rebase -i origin/master

Force push your branch. This allows GitHub to automatically close your pull
request and mark it as merged when your commit(s) are pushed to master. It also
 makes it possible to [find the pull request] that brought in your changes.

    git push --force origin <branch-name>

View a list of new commits. View changed files. Merge branch into master.

    git log origin/master..<branch-name>
    git diff --stat origin/master
    git checkout master
    git merge <branch-name> --ff-only
    git push

Delete your remote feature branch.

    git push origin --delete <branch-name>

Delete your local feature branch.

    git branch --delete <branch-name>

[find the pull request]: http://stackoverflow.com/a/17819027
