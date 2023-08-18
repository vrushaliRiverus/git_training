# git_training
Fork this repo to your private account
## Rebasing and conflict resolution
1. Add a commit to the main branch of your fork
    ```bash
    git checkout main
    echo "a commit to main" > test.txt
    git add test.txt
    git commit -m"a commit to main"
    git push
    ```
2. Create two branches from main
    ```bash
    git checkout -b branch_1
    git checkout -b branch_2
    ```
3. Push a commit on each branch (modify the same line in two different ways)
    ```bash
    git checkout branch_1
    echo "a commit to branch_1" > test.txt
    git add test.txt
    git commit -m"a commit from branch_1"
    git push -u origin branch_1

    git checkout branch_2
    echo "a commit to branch_2" > test.txt
    git add test.txt
    git commit -m"a commit from branch_2"
    git push -u origin branch_2
    ```
4. Create a pull request from first branch to main
5. Rebase merge the first PR (in github webgui)
6. Rebase the second PR with main
    ```bash
    git rebase -i origin/main
    ```
    After conflict resolution `git rebase --continue`
    When rebasing is successful `git push --force-with--lease`
## Commit splitting
### Prep
    ```bash
    git checkout main
    git checkout -b branch_3
    echo "this line should be in first commit" > test.txt
    echo "this line should be in second commit" >> test.txt
    git add test.txt
    git commit -m "this commit needs to be split"
    git push -u origin branch_3
    ```
### Split
    ```bash
    git rebase -i origin/main
    # change 'pick' to 'edit' on the commit
    # save and close
    git reset HEAD~1
    echo "this line should be in first commit" > test.txt
    git add test.txt
    git commit -m "first commit from split"
    echo "this line should be in second commit" >> test.txt
    git add test.txt
    git commit -m "second commit from split"
    git rebase --continue
    git push
    ```
