Documentation contributing guide {How to edit the docs)
============

Interested in updating existing pages or writing your own page? Here you'll learn the basics on contributing to RoR's documentation. This guide assumes you're running Windows, but most steps should be valid on Linux as well. 

## Requirements 
- A GitHub account 
- [GitHub Desktop](https://desktop.github.com/)
- [Git for Windows](https://gitforwindows.org/) (Leave all installer options as the default)
- [Python](https://www.python.org/downloads/) (Make sure the "Add to PATH" option is selected in the installer)

## Forking the repository 
To begin, head over to the [docs.rigsofrods.org GitHub repository](https://github.com/RigsOfRods/docs.rigsofrods.org) and click the ![github-fork](/images/github-fork.png) button at the top right. This will create a copy of the repository on your GitHub account where your changes will be made. 

## Using GitHub Desktop 
After installing GitHub Desktop, launch the app and sign into your GitHub account. After signing in, it'll ask you to clone a repository. Select the repository you cloned earlier along with where you want the repository to be stored locally:

![github-desktop-clone](/images/github-desktop-clone.png)

When the cloning process is finished, it will ask how you plan on using this repository. I recommend selecting "For my own purposes" as this will prevent confusion between your fork and the main repository. 

Click the "Open in Explorer" button to bring you to the repository's files. While holding the Shift key, right click on an empty area of the folder and select "Open PowerShell window here". This is where you'll run the commands in the following steps. 

## Installing MkDocs 
The documentation is powered by MkDocs. it will need to be installed if you wish to be able to preview your changes in real time. Go to the [official MkDocs installation](https://www.mkdocs.org/user-guide/installation/) page and follow the steps listed there, come back here once you've reached the "Installing MkDocs" section. 

After you've successfully installed Python and pip, run the following commands one by one in the PowerShell window you opened earlier: 
```
pip install mkdocs
pip install mkdocs-material
pip install mkdocs-minify-plugin
pip install mkdocs-git-revision-date-localized-plugin
```

These packages can also be found in the `requirements.txt` file in the root of the repository. 

Once everything is installed, you should now be able to view a local version of the docs by running `mkdocs serve`. Your PowerShell window should now look like this:
![powershell-mkdocs](/images/powershell-mkdocs.png) 

The documentation should now be viewable in your browser at `http://127.0.0.1:8000/`

The page will automatically reload when changes are made. 

## Making changes 

In GitHub Desktop, it is **highly** recommended that you create a new branch by selecting `Branch -> New branch...` in the toolbar. This will ensure you don't make changes you didn't want to the main branch, as undoing them can be a pain without creating unnecessary commits. 

Pages are written in Markdown, the same formatting syntax used on GitHub. See [this page](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) to learn the basic Markdown syntax. 

### Adding images 

To add a new image to a page, add the image to the `source\images` folder:
![explorer-images-folder](/images/explorer-images-folder.png)

Give the image a name that describes what the image is of (example for the above image: `explorer-images-folder.png`) Then reference the image in the page using this syntax:
 ```
 ![explorer-images-folder](/images/explorer-images-folder.png)
 ```
 
**Note:** It seems in recent versions of MkDocs, the `mkdocs serve` command can crash after adding an image to the folder. Just run it again if this happens to you. 

### Creating new pages 

To create a new page, simply create a new file with the `.md` file extension in the appropriate category folder. 

Make sure you also add the page to the sidebar by editing `mkdocs.yml`, otherwise `mkdocs serve` will show a warning!

## Making a pull request 

Once you're finished editing, your GitHub Desktop app will probably look similar to this:
![github-desktop-docs](/images/github-desktop-docs.png)

Write a title and description for your changes, then click "Commit to reponame" to submit your changes to the branch. 
