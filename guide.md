# VersionPress Workshop 

Your workshop site ID is **{{siteid}}**.

Useful links:

| Path | Description |
|----- | ---- |
| [/live](/live) | Live site. Username: `admin`, password: `{{siteid}}` |
| [/staging](/staging) | Staging site once you create it. Same username / password |
| [/ssh](/ssh) | SSH web console. Username: `admin`, password: `admin` (sudo allowed) |
| [/db](/ssh) | Adminer. Username `{{siteid}}`, password `{{siteid}}` |



## 1 – Install and activate VersionPress

The goal is to get used to the environment and install & activate VersionPress.

- [ ] Log in to your [SSH console](/ssh). Username: `admin`, password: `admin`.
- [ ] Run `cd live`.
- [ ] Run `wp plugin install ../versionpress-2.2.zip`.
- [ ] [Log in](/live/wp-admin) to the live site. Username: `admin`, password: `{{siteid}}`.
- [ ] Activate VersionPress, finish the full activation.
- [ ] Dismiss the welcome message.

You should now see a table with two rows – *commits*.


## 2 – Change tracking, inspecting history

Here you'll make some actions and inspect how VersionPress tracks them. 

- [ ] Play with the site. Try e.g. there actions:
    - [ ] Update the site title
    - [ ] Add a post named "Workshop" with any content you like
    - [ ] Delete the *Hello Dolly* plugin
- [ ] Go to VersionPress admin page and inspect the changes
    - [ ] Click on the table rows, try *Overview* and *Full diff* modes 

Let's view the same changes via pure Git.
    
- [ ] Switch to your SSH console and run `git log --oneline`
- [ ] Find the commit that created a post draft and run `git show <commit>`

Let's create a commit manually.

- [ ] Let's edit a `header.php` template. Run `nano wp-content/themes/twentysixteen/header.php`.
- [ ] Add `<h1 style="color: red;">Added manually</h1>` right after the `<body>` tag.
- [ ] Save the file: Ctrl + X, answer "Y", then Enter.
- [ ] Check the [live site](/live) that the change is visible

Now you can commit this change either via WP admin or via command line. Choose one.

**GUI option**:

- [ ] Go to WP admin > VersionPress
- [ ] Commit using the form above the main table

**Command-line option**:

- [ ] Run `git config --global user.email "you@example.com"`
- [ ] Run `git config --global user.name "Your Name"`
- [ ] Back in SSH, run `git status`. Git will tell you that there is a file modified.
- [ ] Run `git add .` (note the dot) to stage the file
- [ ] Run `git commit -m "Updated template"` to commit the change
- [ ] Run `git log --oneline` again to see the new commit
- [ ] See the same commit in the WP admin

VersionPress is true Git. No emulation, no pseudo-versioning.


## 3 – Undoing changes

- [ ] In WP admin, click *Undo this* for the ugly red thing we added in the last step.
- [ ] Visit the live site to see that the change is gone.
- [ ] Let's try **selective undo**. Click *Undo this* for the `blogname` update. All newer changes have been maintained.
- [ ] **Undo the undo**. Click the Undo button in the top-most row to get the previous `blogname` again. 

Let's try rollback.

- [ ] Roll back to the original state. Click *Roll back to this* for the bottom-most commit.
- [ ] Undo the rollback again.

You can do this with any action.



## 4 – Basic cloning & merging

Let's try the Holy Grail of WordPress workflows – proper **staging**. 

First, let's **clone** the site.

- [ ] Go to SSH console, make sure you're in the `~/live` folder.
- [ ] Run `wp vp clone --name=staging`. For this workshop, the name must be `staging`.
- [ ] Ctrl + click on the URL given to open a new tab with the [staging site](/staging).
- [ ] Log into the staging site (username: `admin`, password: `{{siteid}}`) and do some updates there:
    - [ ] Create a post titled "Created in STAGING".
    - [ ] Switch a theme to TwentyFifteen
- [ ] On the live site, create a post "Created in LIVE".
- [ ] Let's merge the changes. In SSH, run `wp vp pull --from=staging`.

On your live site, the changes from both environments should be merged.


## 5 – Pushing changes

Because `pull` might possibly create a merge conflict, it's better to run the `pull` inside the staging site and only push the changes into LIVE. Let's try it:

- [ ] Run `cd ../staging`
- [ ] Run `wp vp pull` (the clone knows where to pull from, no need for the `--from` parameter)
- [ ] In the staging site, update the site title (blogname)
- [ ] Run `wp vp push`

The site title has been pushed from staging to the live site.


:tada: **Congratulations!** You've successfully tried the basics of VersionPress. You can learn more at <http://versionpress.net/>.


## Advanced lessons (OPTIONAL)

If you don't have enough, here are some optional, advanced lessons:

### Conflict resolution

If you know how to resolve conflicts in Git, try this:

- [ ] Create a real conflict. For example, edit a `blogname` on both environments at the same time.
- [ ] Try `wp vp pull`. It will warn you about the conflict.
- [ ] Resolve the conflict in Git and commit your changes.
- [ ] Run `wp vp apply-changes` to fix the website. It should now display fine with the conflict resolved.

More on conflict resolution in [this blog post](http://blog.versionpress.net/2015/09/versionpress-2-0-staging/).


### Local branching

You are not limited by our GUI. For example, VersionPress currently doesn't support local branches but you can easily use them via Git:

- [ ] Create a local branch (no clone)
- [ ] Do any changes you like in it
- [ ] Merge your branch back to master using Git
- [ ] Run `wp vp apply-changes` to update the site's database
