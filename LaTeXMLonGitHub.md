

# (DRAFT THIS IS NOT YET WORKING) Using LaTeXML directly with GitHub and/or Overleaf

These instructions may be advanced for some, but may also be easier than installing LaTeXML on your own computer.

## Making a copy of this template on GitHub

On your GitHub account create a new repository.  Do NOT initialize with README / license / gitignore.  Take note of the address which will be something like

```
https://github.com/your-username/my-repo.git
```

From the command line

```
github clone https://github.com/juliusross1/Accessible-LaTeX-Thesis-Template.git
cd Accessible-LaTeX-Thesis-Template
git remote set-url origin https://github.com/your-username/my-repo.git
git push -u origin main
```

Note: If you are using a Personal Access Token (PAT) to use github then you must make sure that "workflows" is enabled in your PAT.

If you are familiar with git you can now use this repository with whatever tools you normally use.  Or you may want to user overleaf (see below).

## Running LaTeXML within GitHub

This seems to be working well.  The only issue is that it can be rather slow to run which is annoying when trying to fix bugs.

Go to your template repository and selection ``Actions".  You should see "Run LaTeXML" on the left hand side.   Click on this and then select "Run Workflow" which takes around 2 minutes (possibly longer when the file gets longer). If there are errors you can find them through the links on this page.

If there are no errors you get the relevant documents inside the /docs folder on your github repository.  It will also create an epub verstion called thesis.epub.

## A convenient way to view the output using GitHub pages

From your repository go to  Settings -> Pages.  Then select "Deploy from Branch"
and below that main -> /docs

After a moment refresh that page and you will be given the link to your website on the top where you can see your document.

Note: The free tier of GitHub does not allow pages for private repositories.

## Using Overleaf

If you are a premium subscriber to overleaf then you can connect overleaf to your github repository.  See [Overleaf's GitHub Integration documentation](https://docs.overleaf.com/integrations-and-add-ons/git-integration-and-github-synchronization/git-integration) for details.
