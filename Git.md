**Authors**: [Alberto F. Martin](https://research.monash.edu/en/persons/alberto-f-martin), [Santiago Badia](https://research.monash.edu/en/persons/santiago-badia-rodriguez)

    - [1.10. Working alone. The commit+push cycle](#110-working-alone-the-commitpush-cycle)
    - [1.11. Working collaboratively](#111-working-collaboratively)
        - [1.11.1. Branching](#1111-branching)
        - [1.11.2. Push a branch to the remote repository at GitHub](#1112-push-a-branch-to-the-remote-repository-at-github)
        - [1.11.3. Create a Pull Request](#1113-create-a-pull-request)
        - [1.11.4. Merge a Pull Request](#1114-merge-a-pull-request)
        - [1.11.5. Pulling changes from the remote repository](#1115-pulling-changes-from-the-remote-repository)
        - [1.11.6. Conflicting changes](#1116-conflicting-changes)
    - [1.12. Conclusions and further references](#112-conclusions-references)
There are a number of reasons ([some of them quite technical](https://git-scm.com/about) to be entirely grasped at this point), but the most important are perhaps the following ones. Git achieves **a sound balance** among speed, efficiency, reliability, and ease-of-use. Indeed, this hallmark of Git has positioned it to be undoubtedly the de-facto standard VCS  used in ([open source](https://opensource.com/resources/what-open-source)) scientific (and not necessarily scientific) software projects. Git was originally developed in 2005 by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds), the same individual who created the Linux OS, i.e., an open source variant of Unix.  Therefore, it is also (as could not be otherwise) **[free and open source](https://git-scm.com/about/free-and-open-source)**. Since then, its popularity has increased significantly, mostly due to the development of repository hosting services in the Cloud such as  [GitHub](https://github.com/), [Gitlab](https://about.gitlab.com/), or [BitBucket](https://en.wikipedia.org/wiki/Bitbucket). Indeed, **virtually the whole state-of-the-art in open source (scientific and not necessarily scientific) software is available at these Git repository hosting services**. Finally, it is worth mentioning that Git is available on multiple platforms, including Microsoft Windows, Linux, or macOS, among others.
When we use Git on a new computer for the first time, we need to set up a few one-time initial configuration options. The very minimal one-time options to be set up to start using Git are: our name, our email address, and our preferred command-line text editor. This is achieved by means of the following three Git commands, respectively:
where you have to replace "`Given name(s) Family name`" by your own names, and `"myname@monash.edu"` by your actual Monash e-mail address. The values provided to the `user.name` and `user.email` options are used by Git in order to identify the changes that you perform on the repository files by your name and e-mail address. Indeed, as we will see in [Section 1.6](#16-the-concept-of-staging-area-creating-our-first-commit), each time that you save a set of changes, i.e., each time that you create a new "commit", your name and e-mail address will be associated to these changes. This becomes especially helpful when you are collaborating with others. Later on in this tutorial, we will be interacting with GitHub. Therefore, **the email address provided should ideally be the same as we will use later in order to set up your GitHub account, e.g., your Monash e-mail address**. We note that the provided names and e-mail address will be viewable in any projects that you ship to the public, e.g., in GitHub, so please do not accidentally expose any information that you would rather like to keep private.
On the other hand, the value provided to the `core.editor` tells Git which command-line editor to be used. In particular, the editor is called by Git whenever it requires that you associate a message to a newly created commit; see [Section 1.6](#16-the-concept-of-staging-area-creating-our-first-commit). In the command above, we are telling Git to use the GNU `nano` editor, which we covered in the [previous tutorial](./Unix-CLI.md#brief-introduction-to-the-gnu-nano-command-line-text-editor). Finally, it is important to mention that the three commands we just ran only need to be run once: the flag `--global` tells Git to use the settings for every project, in your user account, on this computer. You can change your configuration as many times as you want: use the same commands to choose another editor or update your email address.
We will just create a single `README.md` file written in the [*Markdown language*](https://en.wikipedia.org/wiki/Markdown). Markdown is used by GitHub as a very simple way to format text on the web. We will only use the very basic features of Markdown, such as formatting words as bold or italic, adding images, and creating lists. The 3-minute tutorial available [here](https://guides.github.com/features/mastering-markdown/) is helpful in order to get started GitHub Markdown.
> * Add `file1.txt` to staging area. Confirm that you succeeded using `git  status`.
> * Add `file2.txt` to staging area. Confirm that you succeeded using `git  status`.
> * Now run `git commit` **without the `-m` option**. A GNU nano editor will be run in order to let you edit the commit's message. Use your `nano` skills to add an appropriate message, save, and quit.
> * Use `git log` to confirm that you succeeded creating the previous two commits.
At this point we are faced with two options (that are indeed pointed out by the very helpful output of `git status`). We can either discard unstaged changes, or add them to the staging area. We will opt for the first option. In order to do so, we have to use the `git checkout` Git command as follows:
Note that, after using `git checkout`, there are no unstaged changes anymore, i.e., the second line that we added to `README.md` is no longer there. We finish this section by creating a new commit including git c the only change that we finally included in the staging area, i.e., to put "example" in bold face:
If you do not have already a GitHub account linked to your Monash e-mail, please open a new one by visiting the [GitHub signup page](https://github.com/join). Use preferably the same e-mail address that you previously used in [Section 1.6](#16-the-concept-of-staging-area-creating-our-first-commit), e.g., your Monash e-mail address. This is not actually mandatory, but highly recommended, as this set up will allow GitHub to link your Git activity (e.g., commits) to your GitHub user.
> *__Note:__* In the likely case you do not fully understand what the `ssh-keygen` command does, nor what do their flags and arguments mean, that is ok, even if you are not 100% sure of what you are doing. It is important that you acquire the ability to follow a list of commands even without completely understanding them. If you are interested, you can read more about SSH keys [here](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh). 
> *__Note:__* When generating the private key above, we did not actually provide any passphrase, we just hit the Return key, which means no passphrase. However, it is, in general, **highly recommended** to have a  passphrase. The passphrase is used as an additional protection of your private key in case it is stolen. In particular, it is used to cipher the contents of the private key before storing it into the `id_rsa` file. We did not actually use it for simplicity, i.e., in order to avoid Git asking it in the command-line each time that we have to interact with GitHub.
If the command succeeded, there should be (at least) two different files in the `~/.ssh/` folder named `id_rsa` and `id_rsa.pub`:
The former file (`id_rsa`) contains the private key, while the latter (`id_rsa.pub`) the public one.  **You should never expose nor send to anyone the private key** (note indeed its very restrictive file permissions). On the other hand, the public key can be shared with anyone, i.e., GitHub in our case. 
We want to populate our fresh Git repository at GitHub with the contents of the **local** Git repository that we created from the Cygwin terminal in [Section 1.5](#15-creating-a-local-git-repository). In order to do so, we have to execute in the Cygwin terminal the commands shown under the *"... or push an existing repository from the command line"* header in [Figure 6](fig:github_new_repo) . That is, we want to push our local repository up to GitHub. The exact commands will be tailored to your personal account name. In our case, the commands to be executed are:
Of course, you should replace `amartinhuertas` by your GitHub actual username. These two commands set GitHub as the **origin** remote repository of the local Git repository and then push the full (local) repository there, respectively. The **origin** is the default remote repository that one interacts with when you do not explicitly specify a remote repository in a git command. (We note that a local repository might be connected to several remote repositories.)  The `-u` option to `git push` sets GitHub as the upstream repository, which
If pushing succeeded, then, after re-loading `https://github.com/your_github_username/repository4sci1022` on your web browser, you should be able to see an screen similar to that shown in [Figure 7](fig:github_after_push).
The first step to start contributing to a project (e.g., [a scientific computing software package](https://github.com/nschloe/awesome-scientific-computing)) hosted on a Cloud service such as GitHub,  consists on performing an operation referred to as "cloning a remote repository". This is achieved by means of the `git clone` command. This operation **fully copies all files and folders and project history stored in a remote repository into a new directory on the local file system**. This new directory becomes itself a full repository. (Recall, from [Section 1.1](#11-version-control-in-a-nutshell), that Git is a distributed VCS.) 
One of the most useful features of Git is its ability to let us recover from errors that would otherwise be **catastrophic**. Perhaps the most serious mess that one can make is to (unintentionally) remove the local folder containing the Git repository. In our particular scenario, as we do not have local changes to be staged, changes stagged, nor commits pending to be pushed to the remote repository at GitHub, this would not lead to lost work, as we can clone the remote version of the repository from GitHub. Therefore, let us (intentionally) remove our project's local Git repository (because of obvious reasons, **please be extremely careful** to ensure that you type exactly the commands in the next box, and **not**, e.g, `rm -Rf ~/`):
The first argument to the `git clone` is the clone URL (yours will differ, replace `amartinhuertas` by your GitHub username). The clone URL of a project in GitHub can be obtained from the home page of the project, as shown in [Figure 8](fig:github_clone_url).  
By default, `git clone` uses the repository name for the local folder that it creates in order to hold the repository data, i.e., `repository4sci1022` in our case. This default behaviour can be overridden if one provides a second argument to `git clone` with the name desired for the local folder to be created as part of the cloning process.
----

## 1.10. Working alone. The commit+push cycle
<a id="markdown-working-alone-the-commitpush-cycle" name="working-alone-the-commitpush-cycle"></a>

If you are working alone in your project, it is recommended your Git workflow to be based on the commit+push cycle. Essentially, you do some local work, you commit that work (e.g., when you have reached a natural stop, or when you have made enough changes to start worrying about losing them), and then push that commit to **origin**, i.e., the (default) remote repository to which your local repository is linked with.  If you want some advice regarding to the "when to make a commit" dilemma, we recommend, e.g., [this article](https://medium.com/walmartlabs/check-out-these-5-git-tips-before-your-next-commit-c1c7a5ae34d1), although there are many other articles with best practices related to this topic that you may easily find using Google.

To illustrate the commit+push cycle, let us perform a pair of cycle iterations. In particular, let us add to the `README.md` file an image containing a portrait of [William Shakespeare](https://en.wikipedia.org/wiki/William_Shakespeare) that we will borrow from Wikipedia. To this end, we will create a new folder, , called `figures`, in the ls
local Git repository where we will store the image with the portrait.  Then, we will add a link  to that image in the `README.md` file.  We will split this work into two commits, in the first we will add the folder and the image and, in the second, we will modify the `README.md` file. After each commit, we will be invoking `git push` to send our progress to the remote repository at GitHub.  

The commands required to carry out the first iteration are (i.e., create the `figures` folder, download the image from the Internet into the new folder, add the whole folder to the staging area, commit, and push):

We note that it is not strictly necessary to follow the commit+push cycle. You can, e.g., perform 10 consecutive local commits, and then push them in one shot using a single `git push` command. However, we believe it is a good idea to get in the habit of pushing up to the remote repository frequently, as it serves as a guaranteed backup of the project while also allowing collaborators to "pull" in any
changes, as we will see in the next section.

```bash
$ cd ~/Documents/repository4sci1022
$ mkdir figures
$ curl https://upload.wikimedia.org/wikipedia/commons/thumb/a/a2/Shakespeare.jpg/220px-Shakespeare.jpg -o figures/shakespeare_portrait.jpg
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 13577  100 13577    0     0   7492      0  0:00:01  0:00:01 --:--:--  7505
$ git add figures
$ git commit -m "Added W. Shakespeare's portrait image file"
$ git push origin
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 13.37 KiB | 15.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0)
To github.com:amartinhuertas/repository4sci1022.git
   25ab4de..6f9a119  master -> master
```

In the last command, we explicitly tell `git push` to push the new commit to the **origin** remote repository. However, as mentioned before, origin is the default repository one interacts with if no remote repository is specified. Thus, if we replaced the `git push origin` by `git push` in the previous box we would be achieving exactly the same result. 


> *__Exercise 7:__*
By refreshing the GitHub repository in your browser, confirm the presence of the new file by clicking on the `figures` directory link, and then on the `shakespeare_portrait.jpg` image file.

The commands required to carry out the second iteration are (i.e., edit the `README.md` file as shown below, add the changes to the index, commit, and push):

```bash
$ cd ~/Documents/repository4sci1022
$ nano README.md
$ cat README.md
This is an **example** README.md file

![fig:shakespeare](figures/shakespeare_portrait.jpg)

Figure 1. The Chandos portrait (held by the National Portrait Gallery, London)
$ git add README.md
$ git commit -m "Added Shakespeare's image to README.md"
$ git push
```

> *__Exercise 8:__*
By refreshing the GitHub repository in your browser, confirm the presence 
of Shakespeare's portrait on the home page of the project.

## 1.11. Working collaboratively
<a id="markdown-working-collaboratively" name="working-collaboratively"></a>

### 1.11.1. Branching
<a id="markdown-branching" name="branching"></a>

One of the most powerful features of Git is its ability to make **branches**, which you can think of as complete self-contained copies of the project data. With a branch you can make your changes to the project in isolation from the main version of the project, and then merge your changes in only when they are done. This is especially helpful when collaborating with other users; having a separate branch lets you make changes independently from other contributors, reducing the risk of accidental conflicts. Besides, for obvious reasons, when you collaborate in a third-party project, **it is very unlikely that you are allowed to directly push into the master version of the project**.  In the previous section we were allowed to do that only because we were project owners. 

We will use the addition of a second image to the `README.md` file as an example of how to use Git branches. Our first step is to use `git checkout` with the `-b` option, which makes a
new branch and checks it out at the same time:

```
$ git checkout -b add_shakespeare_sonnets
Switched to a new branch 'add_shakespeare_sonnets'
$ 
``` 
We have called the branch `add_shakespeare_sonnets` as we will include in the `README.md` file an image of the cover from the [1609's edition of Shake-Speares Sonnets](https://en.wikipedia.org/wiki/Shakespeare%27s_sonnets)  file.  Using the `git branch` command:

```
$ git branch
* add_shakespeare_sonnets
  master
```

we can list all branches currently defined on the **local Git repository**. The asterisk `*` indicates the currently checked-out branch. Please note that, at this point, the remote repository knows nothing about the existence of this new branch. Having checked out the branch, we are now ready to start making some changes to our working directory.

> *__Exercise 9:__* Download the image at hand from the Internet into the `figures/` folder, edit the `README.md` file to include the image downloaded in the previous step, add the new image and the changes of `README.md` to the staging area, and create a new commit.
*Hint*: the image to be added is available at the following URL: https://upload.wikimedia.org/wikipedia/commons/thumb/f/f6/Sonnets1609titlepage.jpg/220px-Sonnets1609titlepage.jpg

After this commit, the `add_shakespeare_sonnets` has diverged from `master`. The former branch contains a commit that the latter branch does not.  We finished making changes, so we are ready to merge the  `add_shakespeare_sonnets` branch back into the `master` branch. Before merging, we can see the whole set of changes performed using `git diff`. 
We saw in [Section 1.7](#17-modifying-an-already-tracked-file-viewing-the-diff) that this command can be used to see the difference between the unstaged and the staged version of a file, but the same command can be
used to show differences between branches. This particular command is of  the form `git diff branch-1 branch-2`, but if you leave the branch unspecified Git automatically reports the differences against the current branch. This means we can compare `add_shakespeare_sonnets` and `master` as follows:

```bash
$ git diff master
diff --git a/README.md b/README.md
index c88e36f..67275b2 100644
--- a/README.md
+++ b/README.md
@@ -3,3 +3,8 @@ This is an **example** README.md file
 ![fig:shakespeare](figures/shakespeare_portrait.jpg)
 
 Figure 1. The Chandos portrait (held by the National Portrait Gallery, London)
+
+
+![fig:shakespeare_sonnets](figures/shakespeare_sonnets.jpg)
+
+Figure 2. Title page from 1609 edition of Shake-Speares Sonnets.
\ No newline at end of file
diff --git a/figures/shakespeare_sonnets.jpg b/figures/shakespeare_sonnets.jpg
new file mode 100644
index 0000000..5baee82
Binary files /dev/null and b/figures/shakespeare_sonnets.jpg differ
```

Where the `+` sign denotes the lines that were added to `README.md` in order to solve Exercise 9.


### 1.11.2. Push a branch to the remote repository at GitHub
<a id="markdown-push-a-branch-to-the-remote-repository-at-github" name="push-a-branch-to-the-remote-repository-at-github"></a>

Now we will push the local branch  `add_shakespeare_sonnets` to the remote GitHub repository. This allows other people to see the changes you have made. Once the branch is available at the remote repository, and **as far as the changes in it are approved by the repository owner**, the changes can then be merged into the `master` branch. To push the changes onto a new branch on GitHub, we can run the following command:

```bash
$ git push origin add_shakespeare_sonnets
Counting objects: 5, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 24.58 KiB | 6.14 MiB/s, done.
Total 5 (delta 0), reused 0 (delta 0)
remote: 
remote: Create a pull request for 'add_shakespeare_sonnets' on GitHub by visiting:
remote:      https://github.com/amartinhuertas/repository4sci1022/pull/new/add_shakespeare_sonnets
remote: 
To github.com:amartinhuertas/repository4sci1022.git
 * [new branch]      add_shakespeare_sonnets -> add_shakespeare_sonnets
```

As a result, the branch is automatically created on the remote repository.
If you refresh the GitHub page at your browser, you will see a note saying that a branch has just been pushed into the repository. You can also click the "2 branches" link to see your branch listed there. See [Figure 8](fig:fig_branch_pushed).

<a name="fig_branch_pushed"></a> ![fig:fig_branch_pushed](figures/branch_pushed.png) 
Figure 8. The GitHub project home page right after pushing the `add_shakespeare_sonnets` branch.


----
> *__Exercise 10:__*
> On the GitHub page for your project, click on the "Branch: master" drop-down list, and select the  `add_shakespeare_sonnets` branch. Confirm that this branch has an additional commit compared to `master`, and the presence of the cover from the 1609's edition of Shake-Speares Sonnets on the home page of the project.
----

> *__Note:__* While we are following these steps using a single GitHub account, we ask you to make the effort to think as if these steps where followed by a collaborator of us that wants to add new contents to the main page of our project or, otherwise, ourselves adding content to the `README.md` file corresponding to the project of our collaborator.


### 1.11.3. Create a Pull Request
<a id="markdown-create-a-pull-request" name="create-a-pull-request"></a>

A pull request (PR) is a way to alert the GitHub repository owner(s) that you want to make some changes to their project. It allows them to **review the changes proposed** and make sure that they look the way they should before before merging them on the `master` branch.
In order to create a PR, click on the "Compare & pull request" green button shown in [Figure 8](fig:fig_branch_pushed). This leads to the page shown in [Figure 9](fig:fig_pr_create)

<a name="fig_pr_create"></a> ![fig:fig_pr_create](figures/github_create_pr.png) 
Figure 9. The create PR page.

In general, it is desirable to write a thorough report of the changes to be merged. We, nevertheless, skip this step, as the title suggested by GitHub is already an accurate description of the PR. In order to create the PR, we have to click on the "Create pull request" button. This leads you to the page shown in [Figure 10](fig:fig_pr).

<a name="fig_pr"></a> ![fig:fig_pr](figures/pr_page.png) 
Figure 10. The PR page.

You will see a big green button at the bottom that says "Merge pull request". Clicking this will merge your changes into the `master` branch. Sometimes you will be a co-owner or the sole owner of a Git repository, in which case you may not need to create a PR to merge your changes. However, it is still a best practice to make one so you can keep a more complete history of your updates and to make sure you always create a new branch when making changes.

> *__Note:__* Sometimes it is not possible to automatically merge the PR. This means you are faced with a **merge conflict**. This happens when someone has made changes in the target branch of the PR (the `master` branch in our case) that conflict with your changes. In such an scenario, Git cannot figure out automatically which version to use. Therefore, you will have to manually tell Git which version to use.
[Section 1.11.6](#1116-conflicting-changes) introduces the solution of conflicting changes.


### 1.11.4. Merge a Pull Request
<a id="markdown-merge-a-pull-request" name="merge-a-pull-request"></a>

Go ahead and click the green "Merge pull request" button. This will merge your changes into the `master` branch. When you are done, I recommend deleting your branch (too many branches can become messy), so hit the grey "Delete branch" button as well.

----
> *__Exercise 11:__*
> On the GitHub page for your project, click on the "Branch: master" drop-down list, and confirm that there is no longer a   `add_shakespeare_sonnets` branch. Check that the `master` branch now has the commit performed in the `add_shakespeare_sonnets` branch, and that the cover from the 1609's edition of Shake-Speares Sonnets is already on the home page of the project.
----


### 1.11.5. Pulling changes from the remote repository
<a id="markdown-pulling-changes-from-the-remote-repository" name="pulling-changes-from-the-remote-repository"></a>

Right now, the remote repository on GitHub looks a little different than the local one that is available on the Cygwin terminal. For example, the commit we made in  `add_shakespeare_sonnets` branch and merged into the `master` branch does not exist in the `master` branch of the local repository. Besides, the `add_shakespeare_sonnets` does no longer exist in the GitHub repository, but it does on the local one.

As the `add_shakespeare_sonnets` branch does not exist on the GitHub repository, it is reasonable that we first checkout the local `master` branch. This is achieved as follows:

```bash
$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
```


----
> *__Exercise 12:__*
> Use `git log` to check that the commit history for the branch `master` on the local repository does not include the latest ones that can be nevertheless seen in the GitHub page for your project.
----


In order to get the most recent changes that you or others have merged on GitHub's `master` branch, use the following `git pull` command:

```bash
$ git pull origin master
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), done.
From github.com:amartinhuertas/repository4sci1022
 * branch            master     -> FETCH_HEAD
   695b352..ef9f5c1  master     -> origin/master
Updating 695b352..ef9f5c1
Fast-forward
 README.md                       |   5 +++++
 figures/shakespeare_sonnets.jpg | Bin 0 -> 24527 bytes
 2 files changed, 5 insertions(+)
 create mode 100644 figures/shakespeare_sonnets.jpg
```

The output of the command shows all the files that have changed and how they have changed, e.g., `5 +++++` means that 5 lines were added to the file `README.md`.

----
> *__Exercise 13:__*
> Use `git log` to confirm that the commit history for the branch `master` on the local repository **now** matches the one that can be seen in the GitHub page for your project.
----

If you type `git branch`, then you will observe that the `add_shakespeare_sonnets` already exists in the local Git repository.
We can delete this local branch as well. To this end, we can execute the following command:

```bash
$ git branch -d add_shakespeare_sonnets
Deleted branch add_shakespeare_sonnets (was 87919f2).
```

----
> *__Exercise 14:__*
> Write a Git command to confirm that the `add_shakespeare_sonnets` has been deleted from the local repository. 
----


### 1.11.6. Conflicting changes
<a id="markdown-conflicting-changes" name="conflicting-changes"></a>

Even though Git merge algorithms can often automatically figure out how to combine changes from different collaborators, sometimes there is no way of avoiding a conflict. Let us illustrate the concept of conflicting changes and how to resolve them with an example. Let us assume that we are not happy with the current status of the `README.md`. In particular, we would like to change the format of the "example" word, and remove from it the boldface. To this end, we edit the `README.md` and remove the trailing and leading `**` from the word "example", and then we commit this change **but we do not push right after the commit**:

```bash
$ nano README.md
$ cat README.md 
This is an example README.md file

![fig:shakespeare](figures/shakespeare_portrait.jpg)

Figure 1. The Chandos portrait (held by the National Portrait Gallery, London)

![fig:shakespeare_sonnets](figures/shakespeare_sonnets.jpg)

Figure 2. Title page from 1609 edition of Shake-Speares Sonnets.
```
```
$ git add README.md
$ git commit -m "The word example no longer in boldface at README.md"
[master 183ac79] The word example no longer in boldface at README.md
 1 file changed, 2 insertions(+), 2 deletions(-)
```

In the meantime, a collaborator of yours that **is not project owner**, is not happy either with the "example" word in boldface. He prefers it to be in italics. As he is not project owner, he is forced to propose the change the PR way. 

----
> *__Exercise 15:__*
> Mimic the workflow that your collaborator will follow in order to propose the aforementioned change via a PR. This workflow is composed of the following 5 steps:
>
> 1. Clone the GitHub repository in a different folder, e.g., in `repository4sci1022_collaborator`
> 2. Create a local branch in your collaborator's copy of the GitHub repository, named, say, `set_example_in_italics_at_readme_file`.
> 3. Edit the `README.md` file using `nano`, and replace "\*\*example\*\*" by "\*example\*", i.e., boldface by italics.
> 4. Add changes to the staging area and create a new commit into the  `set_example_in_italics_at_readme_file` branch.
> 5. Push the branch to the remote repository at GitHub, create a PR from `set_example_in_italics_at_readme_file` to `master` at GitHub, and merge this PR at GitHub.
>
> Before executing step 5, can you advance whether there will be *merge conflict* in this scenario? Why? Why not? *Hint*: at the beginning of the section, we performed local changes and registered them into a new local commit, but **we did not actually push into `master`**.
----

Now move to the original local copy of the remote GitHub repository (we will no longer play the role of your collaborator). If you completed successfully the steps in Exercise 15, you should obverse the following after pulling the latest changes into `master` from the remote repository:

```
$ git pull origin master
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:amartinhuertas/repository4sci1022
 * branch            master     -> FETCH_HEAD
   ef9f5c1..cebc330  master     -> origin/master
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

As indicated in the penultimate line, Git has detected a merge conflict after the pull. The set of files with merge conflicts still to be resolved can be printed on screen using `git status`. We can see the effect of this conflict by viewing the file `README.md` in `nano`, as shown in [Figure 11](fig:nano_conflict). 

<a name="fig_nano_conflict"></a> ![fig:nano_conflict](figures/nano_conflict.png) 
Figure 11. A file with a merge conflict highlighted.

The highlighted text in [Figure 11](fig:nano_conflict) states that there are two conflicting versions of the first line of `README.md`. In the first, i.e., `HEAD` (our local version), the "example" word appears with no special format. In the second, i.e., the one corresponding to our collaborator's commit with hash `cebc330 ...` ,  the "example" word appears in italics. We prefer the word with no format, so that we manually solve the conflict by editing the `README.md` file, with the result shown in [Figure 12](fig:nano_conflict_solved). 

<a name="fig_nano_conflict_solved"></a> ![fig:nano_conflict_solved](figures/nano_conflict_solved.png) 
Figure 11. The file `README.md` with the merge conflict solved.

After saving the file, we can commit the file with the conflict resolved, and, at this point, we are ready to push in to `master` (check it!).
The local `master` branch in the local copy of the repository of our collaborator does not actually reflect this change. Therefore, the last step in our collaborator's workflow would be a `git pull origin master` command. 


----
> *__Final exercise:__*
> Create a PR in the GitHub repository available at the following URL: https://github.com/amartinhuertas/SCI1022_git_final_exercise. The PR should include a single commit with a version of the `README.md` file containing a link to the GitHub repository you have created along the session. The line to add should be of the form: "Given Name(s) Family name GitHub repository is available [here](URL of your repo goes here)". This link will allow us evaluate your progress with the tutorial.
----

## 1.12. Conclusions and further references
<a id="markdown-conclusions-references" name="conclusions-references"></a>

After completing this workshop, we expect you, at the very least, to be able to understand **why Git has to become an absolute must-use tool in your daily workflow**. Indeed, we highly encourage that you use Git to track the code that you will develop during the rest of modules in this subject, and more importantly, along your whole career. There is a lot more to learn. For example, we did not cover most of **error-recovery** techniques of Git. One of the most useful features of Git is its ability to let us recover from errors that would otherwise be catastrophic.
You can learn more about this topic [here](https://medium.com/@i_AnkurBiswas/common-git-mistakes-and-how-to-fix-them-10184cd5fa77) and [here](https://www.git-tower.com/blog/surviving-with-git-videos/).
If you continue down this technical path you will keep getting better at using Git for years to come.

We recommend seeking out additional resources. The Internet is plenty of excellent resources related to Git that you can use in order to expand your current skills. Here are some suggestions:

* [Learn enough Git to be dangerous](https://www.learnenough.com/git-tutorial/getting_started) tutorial by [Michael Hart](https://www.michaelhartl.com/)
* [Version Control with Git](https://swcarpentry.github.io/shell-novice/) workshop by [Software Carpentry](https://software-carpentry.org/lessons/index.html)
* Free [Pro Git book](https://git-scm.com/book/en/v2) by Scott Chacon and Ben Straub 
* [Git tutorials](https://www.atlassian.com/git/tutorials) by Atlassian  ([BitBucket](https://bitbucket.org/) developers)
* [Tower Git tutorials](https://www.git-tower.com/learn/)