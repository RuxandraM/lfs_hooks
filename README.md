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

## Running

The lfs filters were set to track the files with the extension .extension:

    git lfs track '*.extension' 1>/dev/null

( please see .gitattributes)


The idea here is to demonstrate that the index is not updated:
  
    touch data/file1.extension
    git add .

    # This will trigger git-lfs filter-process which tries to install the
    # lfs hooks. It notices the hooks are identical, so it overwrites them.
    # However, the git index is not updated with the new timestamp

    git commit -m "Add a new file"

    # The commit fails because the pre-hooks are checking against the old index

However, in some situations, `git-lfs filter-process` can be triggered by the refresh index operation itself [to be demonstrated]. Which ends up with an out-of-date index right after `git update-index --refresh`.


