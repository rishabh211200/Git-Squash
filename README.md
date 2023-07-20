# Git-Squashing/Editing Commits

## Introduction:
Squashing multiple commits in Azure DevOps is a useful technique to combine multiple commits into a single, more cohesive commit. This helps in maintaining a clean and organized commit history. In this wiki page, we will guide you through the process of squashing commits using the Git terminal in Azure DevOps.

### Prerequisites:
Before proceeding with the squashing process, ensure that you have the following prerequisites:

We prefer you to use Notepad++ as your Git Editor: By configuring Notepad++ as the default editor for Git, you can leverage its advanced features and user-friendly interface while squashing commits. Notepad++ provides syntax highlighting, code folding, and various plugins that can enhance your editing experience within Git. Follow the steps mentioned in this wiki page to squash multiple commits in Azure DevOps using the Git terminal with the added convenience of using Notepad++ as your editor.
### Steps to configure Notepad++ as the default Git editor:

1. Open the Git Bash Terminal.
  
2. Type the following command to configure Notepad++ as the default editor:

        git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"

Note: Make sure to adjust the path to notepad++.exe based on the installation directory of Notepad++ on your system. The above path assumes the default installation location on a 64-bit Windows system.

3. Verify the configuration by checking the Git global settings using the following command:

        git config --global --get core.editor
   
4. This should display the path to Notepad++ if the configuration was successful.
