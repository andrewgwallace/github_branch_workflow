# GitHub Centralized Repository Workflow

I am working with my partner, Penelope. We are going to build a website collaboratively and plan to use a GitHub repo as a central repository. We will create and work on feature branches locally on our machine.

On my local machine, I make a folder called `penelope_adam_website` that will hold the files and folders of the project. I add a basic `index.html` file with simple HTML scaffolding to the folder.

From within the `penelope_adam_website` folder I initialize the folder as a git repository.

```
$ git init
```

I do this only once. This initialization will generate a hidden folder where all of the git magic will be stored. Git will allow me to do many things, including:
*	take snapshots (commits) of my code as I progress
* make branches
* push my code to a remote server (like GitHub)

My git repository is empty. My folder is not. I need to add my files (file in this case) to the staging area and make my first commit.

```
$ git add -A
$ git commit -m "Initial Commit"
```

Now I have a folder set up with a git repository on my machine. Next, I’d like to push the repository to GitHub.

#### GITHUB GUI
I create a new repository on GitHub.

![alt text](create.png "Create Repo")

This generates a unique URL - a location on GitHub for me to push the local repository from my machine.

![alt text](url.png "Repo URL")

#### MY MACHINE
I am going to add this empty GitHub repository URL as a remote and we are going to give it a name of `origin`.

```
$ git remote add origin https://github.com/galvanize-amc/penelope_adam_website.git
```

Next I am going to push my local master branch to the GitHub repository (`origin`). I use the `-u` flag to set the upstream. This sets up the association between the master branch on my local machine and the master branch on origin (the GitHub repo). I can omit the `-u` in future pushes.

```
$ git push -u origin master
```

Now we have our centralized production master on GitHub.

#### GITHUB GUI
I make Penelope a collaborator on the GitHub repo...

![alt text](co.png "Add Collaborator")

This will allow her to push and pull.

We will work on feature branches on our local machines, push them to GitHub, and use pull requests on GitHub.

I am going to add a navigation menu to `index.html` and Penelope is going to add some welcome text and an image.

#### PENELOPE'S MACHINE
Penelope clones the GitHub repository onto her machine and creates and checks out a branch called `add_welcome`.

```
$ git clone https://github.com/galvanize-amc/penelope_adam_website.git
$ cd penelope_adam_website
$ git checkout -b add_welcome
```

She makes changes and commits the code.

```
$ git add -A
$ git commit -m "Add welcome"
```

She continues working. Meanwhile, ...

#### MY MACHINE

I make a branch called `add_nav` on my machine

```
$ git checkout -b add_nav
```

I make the changes to my code and then commit

```
$ git add -A
$ git commit -m "Add navigation menu"
```

I’m finished with my work and am ready to have it pulled into the master branch. I push my add_nav branch to GitHub, setting the upstream for this branch with -u...

```
$ git push -u origin add_nav
```

#### GITHUB GUI
...and make a pull request on GitHub.

![alt text](pull.png "Create Repo")

![alt text](pull2.png "Create Repo")

![alt text](pull3.png "Create Repo")

Penelope gets my request and stops what she is doing. She is going to merge my add_nav into the master branch on GitHub (the central repository). If there aren't any conflicts, she can use the GitHub GUI, but running things locally will allow her to check and test the code.

#### PENELOPE'S MACHINE
First she needs to checkout her local master, update it (pull the GitHub master into her local master), and then pull the add_nav from GitHub into her newly updated master.

```
$ git checkout master
$ git pull
$ git pull origin add_nav
```

Now the updated master is ready to be pushed to `origin`:

```
$ git push origin master
```

This will close the pull request on GitHub.

![alt text](pull4.png "Create Repo")


Now Penelope goes back to finishing the work on her local branch:

```
$ git checkout add_welcome
```

When she is finished and ready to make a pull request, she will make sure she has committed all of the changes on the `add_welcome` branch on her machine and then push this branch to the GitHub repo (`origin`):

```
$ git push -u origin add_welcome
```

#### GITHUB GUI
Then she will make a pull request on GitHub.

![alt text](pull5.png "Create Repo")


#### Merge Conflicts 
Merge conflicts arise when git is unable auto merge. Git generates lines on the affected files that outline the conflict.

Ex.
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
<<<<<<< HEAD
  <nav>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">About</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  </nav>

||||||| merged common ancestors

=======
  <h1>Welcome</h1>
>>>>>>> 4e813e399aeb3ec3e4392f2822ce39a327f23b56
</body>
</html>
```

They are resolved by editing problem file(s) and making a commit. The problem file(s) may open in vim, a command line text editor, by default. You can either use vim or exit vim by pressing Escape and entering

```
:q!
```

You will need to open the problem files with a text editor of your choice, fix the code, and commit the changes.

To read more about this workflow and other workflows, checkout:

[Comparing Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)
