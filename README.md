# Git-Squashing/Editing Commits

## Introduction:
Squashing multiple commits in Azure DevOps is a useful technique to combine multiple commits into a single, more cohesive commit. This helps in maintaining a clean and organized commit history. In this guide, we will walk you through the process of squashing commits using the Git command line interface.

### Prerequisites:
Before proceeding with the squashing process, ensure that you have the following prerequisites:

* Git Installed: Make sure Git is installed on your system. If not, download and install it from the official Git website.
* Repository Setup: Have a Git repository set up with the commits you want to squash. Make sure you are on the branch containing the commits you wish to squash.
* We prefer you to use Notepad++ as your Git Editor: By configuring Notepad++ as the default editor for Git, you can leverage its advanced features and user-friendly interface while squashing commits. Notepad++ provides syntax highlighting, code folding, and various plugins that can enhance your editing experience within Git. Follow the steps mentioned in this wiki page to squash multiple commits in Azure DevOps using the Git terminal with the added convenience of using Notepad++ as your editor.

#### Steps to configure Notepad++ as the default Git editor:

1. Open the Git Bash Terminal.
  
2. Type the following command to configure Notepad++ as the default editor:

        git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"

Note: Make sure to adjust the path to notepad++.exe based on the installation directory of Notepad++ on your system. The above path assumes the default installation location on a 64-bit Windows system.

3. Verify the configuration by checking the Git global settings using the following command:

        git config --global --get core.editor
   
4. This should display the path to Notepad++ if the configuration was successful.


### Steps to Squash Commits, Edit Commits History, Rename Commit Messages :-

#### Step 1: Make sure you are in the right branch (In branch you need to make changes)

![AzureOnlineBranchSS](https://github.com/rishabh211200/Git-Squash/assets/55344761/88f6c8cf-2e6c-4217-934f-082ef50c4d08)

Right here You can see I am into a branch named 959709_BKK_BR_Config_Creation online, And I need to make sure that I am into same branch in my local as well using the below command

    git branch

![CommandPromptGitBranch](https://github.com/rishabh211200/Git-Squash/assets/55344761/587377da-486e-4282-b3ce-2d8ef2ec0b64)

#### Step 2: Identify the Commits

First, identify the range of commits you want to squash. You can use the git log command to view the commit history and find the commit hashes of the commits you want to squash.

    git log

Note down the commit hashes of the commits you want to squash. The oldest commit in the range will be the "base" commit.

![GitLogCMD](https://github.com/rishabh211200/Git-Squash/assets/55344761/92cce4c4-db0e-47cc-9c17-038238f3aab6)

Here, you can see three commits, I am going to make changes in.

#### Step 3: Start an Interactive Rebase

Run the following command to start an interactive rebase:

    git rebase -i <base_commit_hash>^

Replace <base_commit_hash> with the hash of the base commit (the oldest commit in the range). The caret (^) indicates the parent of the base commit.

Here, in our case we are going to make use of HEAD~X, so we are going to pick multiple commits from top, as you can see in git log we are having 3 commits in our branch and we are going to squash 2 recent commits to oldest one. We will be using the below command to pick'em all :-

    git rebase -i HEAD~3

Here 3 represents number of commits you need to pick from top/head.

![git rebase cmd](https://github.com/rishabh211200/Git-Squash/assets/55344761/5f9031c4-8f52-45a5-abab-8c1ba7a90de8)

After we press enter, Notepad++ will be opened as editor like below:

![NotepaddRebaseEditor](https://github.com/rishabh211200/Git-Squash/assets/55344761/0fd316a1-a610-4e2c-bc82-022b6b5b28b8)

In above image you can see in line number 1,2 & 3 we are having our commit messages, At the top we are having oldest one and at bottom we are having latest.
We will be squashing latest and second latest into the oldest.

For doing the same we are going to replace 'pick' with 's'/'squash' for the below 2 commits.
For example, if you have three commits to squash into the base commit, your interactive rebase file might look like this:

![squashNotepad](https://github.com/rishabh211200/Git-Squash/assets/55344761/dfb7746e-d4d5-44b3-8fcb-39ea1d6a2057)

Save and close the rebase editor.

After saving the interactive rebase file, Git will prompt you to edit the commit message for the new combined commit. You can keep the existing commit message or modify it as needed.
Now another notepad++ window will open to make changes in commit message:

![EditCommitMessage](https://github.com/rishabh211200/Git-Squash/assets/55344761/b7ca8408-f496-4d8c-b4ea-8fb28b63fb92)

Here in above image we can see the commit messages we had used previously, Now we are going to make changes to them and make a single commit message.

We will be commenting out the remaining 2 messages or we can remove all messages and write a new one and at last we need to make sure in the whole file we should have only one line un-commented which is going to be new commit message in our branch.

After following the above steps, Save and close the rebase editor. You must see like this:

![SuccessfullyRebased](https://github.com/rishabh211200/Git-Squash/assets/55344761/0fd788fe-f83d-4bc8-aa46-2a4aa17fb083)


#### Step 5: Push the Changes

Now that you've squashed the commits locally, you may need to force-push the changes to the remote repository if the commits were already pushed.

**Note: Be cautious when force-pushing, as it rewrites the commit history. Only do this if you're sure it won't affect others working on the same branch.**

    git push -f

![git push F](https://github.com/rishabh211200/Git-Squash/assets/55344761/5ffaebc4-b2a1-4a6b-b21c-90bec84aaa7b)

and now after force update, you can check online in your Pull Request/Commit History. That must be updated till now.

![Final](https://github.com/rishabh211200/Git-Squash/assets/55344761/9b2a903f-d3a6-4b57-9eda-a7d525dece94)

### Bonus

During an interactive rebase, you can use various "actions" to modify the commit history. These actions are specified in the interactive rebase editor, where you can choose what to do with each commit. Here are the main rebase actions and their purposes:

* **pick** or **p**: This is the default action for each commit in an interactive rebase. It means that the commit will be included as is.

* **reword** or **r**: This action allows you to edit the commit message of the selected commit.

* **edit** or **e**: This action stops the rebase process after applying the selected commit. It allows you to make changes to the files in the commit, amend the commit, and then continue the rebase.

* **squash** or **s**: This action allows you to combine the selected commit with the previous commit. The commit messages will be merged, and you'll be prompted to edit the new commit message.

* **fixup**: This action is similar to squash, but it discards the commit message of the selected commit and keeps the message of the commit it's squashed into.

* **drop** or **d**: This action removes the selected commit from the history. The commit will be skipped, and it won't be included in the final result.

* **exec**: This action allows you to run a shell command after applying the selected commit. It can be useful for automated tasks during the rebase process.

* **label**: This action assigns a label to the selected commit. Labels can be useful for organizing and managing commits during the rebase.

To perform an interactive rebase with these actions, you can use the following command:

    git rebase -i <commit>

Replace **'<commit>'** with the commit before the first commit you want to modify. An editor will open, displaying the list of commits and their actions. Change the action keyword from **'pick'** to the desired action for each commit, save the file, and close the editor to apply the changes.

Keep in mind that rewriting the commit history using rebase actions can alter the commit hashes, so it's essentials to use this feature carefully, especially on shared branches. Always communicate with your team to ensure a smooth collaboration process.


### Conclusion

Congratulations! You've successfully squashed commits in your Git repository. Squashing commits can help keep your commit history clean and concise, making it easier for others to understand the changes in your codebase.

Remember that rewriting history should be done with caution, especially if you're collaborating with other developers. Always communicate and coordinate changes with your team to avoid conflicts and ensure a smooth development process.

Now you can use this knowledge to maintain a clean and organized commit history in your projects. Happy coding!s



    


