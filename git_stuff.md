## Clone a Repo
```bash
git clone git@$GIT_HOST:operation/nagios.git
```

## Adding a file explained
```bash
git pull                -> like: svn up
git add <file>          -> If its a new untracked file
git commit -m'message'  <file>       -> commits the file to your local repo (untracked file)
git push                -> pushes local changes to the source git repo
```

## Update and existing File explained
```bash
git pull
git commit -m'message' -a <file>      -> commits the file to your local repo
git push
```

## Basic change workflow
1. Get the latest changes
```bash
git pull
```
2. Make your change
```bash
vi somefiles
```
3. Make sure your changes are good
```bash
git diff
```
4. Add to the staging area, and commit
```bash
git add somefiles
git commit
```
5. Grab possible changes that happened while you were editing,
..* --rebase is your friend, it will avoid to create a merge commit
```bash
git pull --rebase
```
6.  Push your changes
```bash
git push origin HEAD:refs/for/master
```

##  If you happen to have a conflict
1. Edit the files in conflict
```bash
vi somefiles
```
2. add them, it means "resolve" to git
```bash
git add somefiles
```
3. Resume the rebase
```bash
git rebase --continue
```
4.  And just to make sure you're up to date, do it again
```bash
git pull --rebase
```
5.  Push your changes
```bash
git push origin HEAD:refs/for/master
```

## Permanently remove a file and all history
```bash
git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch [filename]' --prune-empty --tag-name-filter cat -- --all
git push origin --force --all
```

## BRANCH STYLE CHANGES
1. update local copy in master branch
```bash
git pull
```
2. Create branch
```bash
git checkout -b TICKET
```
3. Make changes
4. Add Files
```bash
git add [files]
```
5. Commit
```bash
git commit -m “ticket etc”
```
6. Push
```bash
git push -u origin TICKET
```
7. Go to UI and submit pull request


## Cleanup Branches
### Local
```bash
git branch -D bugfix
```
### Remote
```bash
git push origin --delete <branchName>
```
or
```bash
git push origin :<branchName>
```

## Rebase a branch
```bash
BRANCH=$(git rev-parse --abbrev-ref HEAD 2>/dev/null)
git pull --rebase origin production
git push origin ${BRANCH} --force
```

## reset your local repo to match the remote branch
(this has worked when i need it to, but i haven't tried with branches)
```bash
git reset --hard origin/HEAD
git reset —hard
```


## tagging
from the master branch you want to tag
```bash
git tag -a -m'message' [tag name]
git push origin [tag name]
```

## Using RestAPI to Get list of Team members
# First Find the team API endpoint
```bash
curl -u user:pass https://[github]/api/v3/orgs/[org]/teams/[team]
```
# Then query that team end point with max per page value to see how many pages there are.
```bash
curl -I -u user:pass https://[github]/api/v3/organizations/655/team/250/members?per_page=100
```
# Look for the Link line
# Query each page and dump to output fieles
```bash
curl -u user:pass --output /tmp/joe "https://[github]/api/v3/organizations/655/team/250/members?page=1&per_page=100"
curl -u user:pass --output /tmp/joe2 "https://[github]/api/v3/organizations/655/team/250/members?page=2&per_page=100"
curl -u user:pass --output /tmp/joe3 "https://[github]/api/v3/organizations/655/team/250/members?page=3&per_page=100"
```
