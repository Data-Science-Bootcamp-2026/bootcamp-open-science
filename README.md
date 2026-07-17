# Data Science Bootcamp 2026 (Part 2: Open Science)

- [Book](https://data-science-bootcamp-2026.github.io/bootcamp-open-science/) for detailed notes
    - Download PDF slides by clicking the easel icon on the top left
    - Download PDF version of the book by clicking the PDF document icon on the top left

---

**LEARNING OBJECTIVES:**

- 


---

**WORKSHOP PART 1:**

1. Go to the [book]
2. At the top left, click the GitHub icon (the cat)
3. Near the top right of the GitHub page, click **Fork**
4. Click the green **Create fork** button

You have now created a fork (a copy of a repository that you do not have write access to) on your own GitHub account. You *do* have write access to this forked copy. But this still only lives on the cloud. To download a linked copy locally, we need to clone it.

5. Click the green **<> Code** button
6. Copy the HTTPS URL
7. Open VS Code
8. Click the search bar

<p align="center">
  <img src="docs/assets/images/vscode_searchbar.png" width="400" alt="VS Code searchbar">
</p>

9. Click **Show and Run Commands >**
10. Click **Git: Clone** (if it does not show up, start typing it in to bring it up)
11. Paste the URL and hit Enter
12. Save it; as long as the repo uses relative paths, it generally does not matter where you save it

Let's try using GitHub Copilot:

13. On VS Code, open the right pane (if you do not see a right panel, click the button on the top right of VS Code and it will pop up)

<p align="center">
  <img src="docs/assets/images/github_copilot_pane.png" width="300" alt="GitHub Copilot pane">
</p>

14. In the tab called CHAT (GitHub Copilot), type in this prompt: "Add the learning objectives here."
    - Can you spot why GitHub Copilot knows where 'here' is?
    - GitHub Copilot can 'see' the repo you have open (which contains the contents of the book and slides), so it can figure out what the learning objectives may be.
15. Wait a moment as it thinks of what to do. It will make a suggestion and you can click the blue **Keep** button to accept it. Review and revise as necessary.
16. View your GitHub Copilot usage limits by clicking the icon on the bottom right of VS Code.

<p align="center">
  <img src="docs/assets/images/github_copilot_white.png" width="50" alt="GitHub Copilot logo">
</p>

Let's try changing the license:

17. Go to [choosealicense.com](https://choosealicense.com/)
18. Search through a license that is not the MIT License (because I already have that)
19. Copy the text and paste it into the LICENSE file then save

You've now made several changes to the repo. Let's stage, commit, and push:

20. Go to **Source Control** tab (the third button) on the left sidebar (it should have a blue number '3' on it)
21. There should be 3 changes that can be staged
    - Click through each one and notice how GitHub displays line additions and subtractions
    - Is the file you ignored on this list? If so, you did something wrong!
22. Stage changes by hovering your pointer over the files and click the `+` symbol; let's stage all of them by hovering your pointer over the **Changes** row and click its `+` symbol
23. Commit changes by providing a brief commit message in the free text field and clicking the blue **Commit** button
24. Push changes by clicking the blue **Sync changes ↑** button

This was a simplified version of what you need to do. We skipped some steps like creating a branch (we were working on the `main` branch, which is generally discouraged!). Now let's do it the proper way!

---

**WORKSHOP PART 2:**

Now `origin/main` (remote repo) is up to date. As it happens, `main` is also up to date, but that's only because we skipped making branches -- we'll do that properly below. For now, let's go what to normally do to update `main` if there were actual changes.

1. On VS Code, go to the **Source Control** tab again
2. If `main` is outdated, it would normally show a blue **Sync changes ↓** button and clicking that would update your local `main`. In this case, there wouldn't be, but let's go through the motions anyway by manually pulling it:
    - Hover your pointer over the the **CHANGES** row
    - Click `...`
    - Click **Pull**

Now let's create a branch:

3. Click the **main** on the bottom left of VS Code
4. A dropdown menu will appear from the search bar
5. Click **+ Create a new branch** (this will use your current branch, `main`, as the template) and give your new branch a name
    - Notice the branch name on the bottom left has changed

Let's make a Quarto document using RStudio:

6. Using what you learned in Part 1 of this bootcamp, create an R project for this repo
7. Follow the instructions on [this guide](https://quarto.org/docs/tools/rstudio.html) to create a Quarto document
    - The only thing I would change is, **in the first pop-up, uncheck "Use visual markdown editor"**
    - That option opens the Quarto document in a code-less (view) mode, but it is actually more intuitive to work in the source (edit) mode
    - You can always switch between **Source** and **Visual** modes on the taskbar

<p align="center">
  <img src="docs/assets/images/rstudio_quarto.png" width="300" alt="Quarto viewer">
</p>

8. Save this file in a new folder within the repo called `analysis`
9. Type whatever you want, following common syntax:

| What you want | Markdown syntax |
|---|---|
| Heading | `# Main heading`, `## Subheading` |
| Bold or italics | `**bold**`, `*italics*` |
| Bulleted list | `- Item` |
| Numbered list | `1. Item` |
| Link | `[Text](https://example.com)` |
| Image | `![Caption](image.png)` |
| Inline code | `` `code` `` |
| Code block | Three backticks on the lines before and after the code |

Now let's make sure to record the R dependencies using `renv`:

10. In the R console, run `renv::init()` to initialize
    - If you do not have the `renv` package installed, run `install.packages("renv")` first
    - This creates several things in your repo; check them out:
        - `renv.lock`
        - `.Rprofile`
        - `renv/` folder
11. Try writing `library(tableone)` in an R chunk in your Quarto document and save
    - RStudio will warn you that you need `tableone` but don't have it installed
    - You may be surprised because we used `tableone` in Part 1 of the bootcamp, so why is it saying you don't have it?
    - `renv` creates a project-specific library; this repo is now separated from your default system library for R - this lets you freeze your package versions within this project so it doesn't break when the R and package versions move on outside it
12. Install `readr`
13. Run `renv::status()` to view what needs updating in the snapshot
14. Run `renv::snapshot()` to update `renv.lock`
15. As a check to make sure everything is okay, try running `renv::restore()` to restore the packages; if everything had worked perfectly, there would not be anything new to restore

Now let's stage, commit, and push the changes.

16. Use the steps from earlier to stage and commit the changes
17. The push will be a bit different this time because we created a new branch -- there is no remote version of this branch
    - So instead of a blue **Sync changes ↑** button, you will see a blue **Publish branch** button
17. Go to GitHub and you should see a yellow banner
    - Click the green **Compare & pull request**; a pull request is a proposal to merge changes from one branch to another (in this case, from the new remote branch into the `main` remote branch)
18. Provide a pull request description
19. Click the green **Create pull request** button
20. GitHub will check for merge conflicts
21. Because this is your repo, it is your responsibility to look over the pull request and approve it
    - Click **Merge branch**
    - Click **Delete branch**
22. Go back to VS Code, switch to the `main` branch, and pull the updates
    - If there's no button to do so, manually pull changes by hovering your pointer over the the **CHANGES** row and click its `...` symbol, then **Pull**

And so the cycle continues for future changes! Notice on the **Source Control** tab, under **GRAPH**, you can view the history of this repo.
