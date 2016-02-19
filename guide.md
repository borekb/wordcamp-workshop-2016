# WordCamp Prague 2016

Your workshop site ID is **{{siteid}}**.

- [`/live/`](./live/) site – username: `admin`, password: `{{siteid}}`
- [`/staging/`](./staging/) site (once you create it)
- [SSH web console](./ssh) – username: `admin`, password: `admin`, sudo allowed
- [DB Adminer](./db) – username `{{siteid}}`, password `{{siteid}}`

Useful links:

- [VersionPress 2.2](http://bit.ly/versionpress-2-2) (stable)
- <u>VersionPress 3.0-DEV</u> (development)


## 1 – Install and activate VersionPress

- [ ] Log into the live
- [ ] Install VersionPress
- [ ] Activate it
- [ ] Deactivate via UI
- [ ] Activate again using a WP-CLI command *(if on 3.0; this would be to get used to the command line and try that it works; if we can't use this, skip these last two steps)*


## 2 – Tracking changes

- [ ] Do some actions. *(Specify which ones.)*
- [ ] Inspect them in the UI
- [ ] Inspect them in Git – use the SSH console
- [ ] Create a manual commit in Git
    - [ ] Edit a template
    - [ ] Manually commit the changes
- [ ] Inspect the history again in both Git and admin UI
- [ ] Do the template edit again but this time commit via the GUI


## 3 – Undoing changes

*Generally try a couple of undos, rollbacks, undos of rollbacks etc. To be specified.*


## 4 – Basic cloning & merging

- [ ] Clone to a staging site
- [ ] Visit it, log into it
- [ ] Do some updates on LIVE
- [ ] Do some updates on STAGING
- [ ] Do a pull on LIVE


## 5 – Better cloning & merging

- [ ] The first three steps as above
- [ ] Step into STAGING and run `pull` there
- [ ] Review changes in STAGING
- [ ] Push to LIVE


## 6 – Conflict resolution

*Probably optional, resolving conflicts in Git is quite hard and we could waste time here.*

- [ ] Basically repeat 5 but introduce a conflict
- [ ] Resolve the conflict in Git, commit changes
- [ ] Push to LIVE after the conflict has been resolved


## 7 – Bonus: Local branching

*Bonus lesson to show that VP users are not limited by our GUI.*

- [ ] Create a local branch (no clone)
- [ ] Experiment in it
- [ ] Merge to master & `apply-changes`
