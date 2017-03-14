# Git Workflow & Commands

Repository contains basic branches description and complete command reference on creating, committing merging & deleting Git branches.

## Branches Types

### Main Branches
- **master**<br>
**origin/master** is the main branch where the source code of HEAD always reflects a production-ready state.
- **develop**<br>
**origin/develop** is the main branch where the source code of HEAD always reflects a state with the latest delivered development changes for the next release.

### Support Branches
- **feature/{branch-name}**<br>
Feature branches are used to develop new features for the upcoming or a distant future release.
- **hotfix/{branch-name}**<br>
Hotfix branches are very much like release branches in that they are also meant to prepare for a new production release, albeit unplanned. They arise from the necessity to act immediately upon an undesired state of a live production version.
- **release/{vX.X.X}**<br>
Release branches support preparation of a new production release. They allow for last-minute dotting of i’s and crossing t’s. They allow for minor bug fixes and preparing meta-data for a release (version number, build dates, etc.).

## Branches details

### Feature branches
May branch off from: `develop`<br>
Must merge back into: `develop`<br>
Branch naming convention: `feature/{branch-name}`

#### Creating Feature Branch
```
git checkout -b feature/{branch-name} develop

Increase X."X".X version

git commit -a -m "Added {feature} to ..."
```

### Incorporating a finished feature on develop
```
$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff feature/{branch-name}
Updating ea1b82a..05e9557
(Summary of changes)
$ git branch -d feature/{branch-name}
Deleted branch feature/{branch-name} (was 05e9557).
$ git push -u origin develop
```

### Hotfix branches
May branch off from: `master`<br>
Must merge back into: `master`, `develop`, `release`<br>
Branch naming convention: `hotfix/{branch-name}`

#### Creating Hotfix Branch
```
git checkout -b hotfix/{branch-name} master

Increase X.X."X" version

git commit -a -m "Fixed {hotfix} for ..."
```

### Incorporating a finished feature on develop
```
$ git checkout master
Switched to branch 'master'
$ git merge --no-ff hotfix/{branch-name}
Updating ea1b82a..05e9557
(Summary of changes)
$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff hotfix/{branch-name}
Updating ea1b82a..05e9557
(Summary of changes)
$ git branch -d hotfix/{branch-name}
Deleted branch hotfix/{branch-name} (was 05e9557).
$ git push -u origin master
$ git push -u origin develop
```
