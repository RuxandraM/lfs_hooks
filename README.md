 ## Test hooks

 This is a test to see when the git hooks are overwritten by git-lfs.
 Note that pre-commit is a custom hook, and will not be overwritten by git-lfs.

 This test was done on

     git-lfs/2.13.3
     git version 2.23.0

 ## Set up

In order to track the changes to the git hooks, `.git/hooks` was changed to a symlink 
pointing to a folder in the repo (`git-hooks`). During setup, please run:

     rm -r .git/hooks
     ln -s ../git-hooks .git/hooks

 
