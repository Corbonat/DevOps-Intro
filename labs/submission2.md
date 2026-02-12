**Task 1**:
```
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git cat-file -p 7e4b981dc40a619c47abd2a701f4120367442c95
100644 blob db7abc0be45b7051f5e4d6c5bf99208a9ddf8e7a    README.md
040000 tree a1061247fd38ef2a568735939f86af7b1000f83c    app
040000 tree 788b221a8787de2ff117bef28485d13dd331d9a0    labs
040000 tree d3fb3722b7a867a83efde73c57c49b5ab3e62c63    lectures
100644 blob 418a98ced2ac70b5bdee0be9732ecdaae7264515    test.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git cat-file -p 418a98ced2ac70b5bdee0be9732ecdaae7264515
��Test content
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git cat-file -p 7584bed
tree 7e4b981dc40a619c47abd2a701f4120367442c95
parent 6f044dd2f9c7801441a98988f184093142e90ece
author Iukharev <xxromchikx@gmail.com> 1770928644 +0300
committer Iukharev <xxromchikx@gmail.com> 1770928644 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgXsujz27eG3ameuRXoKVs2vVlOu
 v8JjzSAwMwgnB3PDoAAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQLn8WqrUxN/hxRh5KQE/cqjmZeIozqxnBfOt+mTOeaDM9twx07JFeG8Cyq7+x2HvAv
 cK+3XT6Fjwok6Q6h1DgAs=
 -----END SSH SIGNATURE-----

Add test file
```

Object types:
A blob is the raw content of one file. It does not store the file name.
A tree is a folder snapshot. It stores file/folder names and links them to blobs or other trees.
A commit is a record of one project state. It points to a tree, parent commit(s), and stores author, time, and message.

How Git stores repository data:
Git stores data as objects addressed by hash in .git/objects.
Commits point to trees, and trees point to blobs, so history is a chain of snapshots.
If file content is the same, Git can reuse the same blob instead of creating a new one.

Example object content:
blob (git cat-file -p <blob_hash>):
Test content

tree (git cat-file -p <tree_hash>):
100644 blob <blob_hash> test.txt

commit (git cat-file -p <commit_hash>):
tree <tree_hash>
parent <parent_hash>
author Iukharev Roman xxromchikx@gmail.com
 1000000000 +0300
committer Iukharev Roman xxromchikx@gmail.com
 1000000000 +0300

Add test file

**Task 2:**
```
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> "First commit"  | Out-File -Encoding utf8 file.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git add file.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git commit -m "First commit"
[git-reset-practice 793869d] First commit
 1 file changed, 1 insertion(+)
 create mode 100644 file.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> 
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> "Second commit" | Add-Content file.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git add file.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git commit -m "Second commit"
[git-reset-practice 28539c2] Second commit
 1 file changed, 1 insertion(+)
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> 
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> "Third commit"  | Add-Content file.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git add file.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git commit -m "Third commit"
[git-reset-practice b976f95] Third commit
 1 file changed, 1 insertion(+)
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git log --oneline -3
b976f95 (HEAD -> git-reset-practice) Third commit
28539c2 Second commit
793869d First commit
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git status
On branch git-reset-practice
nothing to commit, working tree clean
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git reset --soft HEAD~1
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git status
On branch git-reset-practice
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   file.txt

PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git log --oneline -3
28539c2 (HEAD -> git-reset-practice) Second commit
793869d First commit
244b41e (origin/feature/lab2, feature/lab2) Task 1 complete
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git reset --hard HEAD~1
HEAD is now at 793869d First commit
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git status
On branch git-reset-practice
nothing to commit, working tree clean
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git log --oneline -3
793869d (HEAD -> git-reset-practice) First commit
244b41e (origin/feature/lab2, feature/lab2) Task 1 complete
7584bed (main) Add test file
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git reflog
793869d (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
28539c2 HEAD@{1}: reset: moving to HEAD~1
793869d (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
28539c2 HEAD@{1}: reset: moving to HEAD~1
b976f95 HEAD@{2}: commit: Third commit
28539c2 HEAD@{3}: commit: Second commit
793869d (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
793869d (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
28539c2 HEAD@{1}: reset: moving to HEAD~1
b976f95 HEAD@{2}: commit: Third commit
793869d (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
28539c2 HEAD@{1}: reset: moving to HEAD~1
b976f95 HEAD@{2}: commit: Third commit
28539c2 HEAD@{3}: commit: Second commit
793869d (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
793869d (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
28539c2 HEAD@{1}: reset: moving to HEAD~1
b976f95 HEAD@{2}: commit: Third commit
28539c2 HEAD@{3}: commit: Second commit
793869d (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
244b41e (origin/feature/lab2, feature/lab2) HEAD@{5}: checkout: moving from feature/lab2 to git-reset-practice
244b41e (origin/feature/lab2, feature/lab2) HEAD@{6}: commit: Task 1 complete
7584bed (main) HEAD@{7}: checkout: moving from main to feature/lab2
7584bed (main) HEAD@{8}: commit: Add test file
6f044dd (upstream/main) HEAD@{9}: reset: moving to upstream/main
4515622 HEAD@{10}: checkout: moving from feature/lab1 to main
0d2540f (origin/feature/lab1, feature/lab1) HEAD@{11}: commit: docs: Finished submissions.md (surly this time)
9b1a595 HEAD@{12}: commit: docs: Finished submissions.md
3995b9d HEAD@{13}: commit: docs: Added .png file with my SSH key on github
fb05349 HEAD@{14}: commit: docs: Added .png file with autofilled template for PR
098f2a6 HEAD@{15}: commit: docs: Added .png file with my verified commit in github
cc3ea7b HEAD@{16}: checkout: moving from main to feature/lab1
4515622 HEAD@{17}: checkout: moving from feature/lab1 to main
cc3ea7b HEAD@{18}: reset: moving to cc3ea7b
226fda5 HEAD@{19}: checkout: moving from main to feature/lab1
4515622 HEAD@{20}: cherry-pick: chore: add PR template
d6b6a03 HEAD@{21}: reset: moving to origin/main
...skipping...
793869d (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
793869d (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
28539c2 HEAD@{1}: reset: moving to HEAD~1
793869d (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
793869d (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
28539c2 HEAD@{1}: reset: moving to HEAD~1
b976f95 HEAD@{2}: commit: Third commit
28539c2 HEAD@{3}: commit: Second commit
793869d (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
244b41e (origin/feature/lab2, feature/lab2) HEAD@{5}: checkout: moving from feature/lab2 to git-reset-practice
244b41e (origin/feature/lab2, feature/lab2) HEAD@{6}: commit: Task 1 complete
7584bed (main) HEAD@{7}: checkout: moving from main to feature/lab2
7584bed (main) HEAD@{8}: commit: Add test file
6f044dd (upstream/main) HEAD@{9}: reset: moving to upstream/main
4515622 HEAD@{10}: checkout: moving from feature/lab1 to main
0d2540f (origin/feature/lab1, feature/lab1) HEAD@{11}: commit: docs: Finished submissions.md (surly this time)
9b1a595 HEAD@{12}: commit: docs: Finished submissions.md
3995b9d HEAD@{13}: commit: docs: Added .png file with my SSH key on github
fb05349 HEAD@{14}: commit: docs: Added .png file with autofilled template for PR
098f2a6 HEAD@{15}: commit: docs: Added .png file with my verified commit in github
cc3ea7b HEAD@{16}: checkout: moving from main to feature/lab1
4515622 HEAD@{17}: checkout: moving from feature/lab1 to main
cc3ea7b HEAD@{18}: reset: moving to cc3ea7b
226fda5 HEAD@{19}: checkout: moving from main to feature/lab1
4515622 HEAD@{20}: cherry-pick: chore: add PR template
d6b6a03 HEAD@{21}: reset: moving to origin/main
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git reset --hard b976f95
HEAD is now at b976f95 Third commit
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git log --oneline -3
b976f95 (HEAD -> git-reset-practice) Third commit
28539c2 Second commit
793869d First commit
```

I created three commits in git-reset-practice: First (793869d), Second (28539c2), and Third (b976f95).
After reset --soft, HEAD moved back from Third to Second, but the changes from the removed commit stayed staged. This means history moved, while index and working tree still kept the change.
After reset --hard, HEAD moved back again to First, and both index and working tree were cleared to match that commit.
I then checked reflog and found b976f95 (Third commit), which allowed me to fully restore the previous state.
This shows that reflog is a reliable recovery tool when commits disappear from normal log after reset.

**Task 3:**
```
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git switch -c side-branch
Switched to a new branch 'side-branch'
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> echo "Branch commit" >> history.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git add history.txt && git commit -m "Side branch commit"
At line:1 char:21
+ git add history.txt && git commit -m "Side branch commit"
+                     ~~
The token '&&' is not a valid statement separator in this version.
    + CategoryInfo          : ParserError: (:) [], ParentContainsErrorRecordException
    + FullyQualifiedErrorId : InvalidEndOfLine

PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git switch -
Switched to branch 'feature/lab2'
Your branch is up to date with 'origin/feature/lab2'.
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git switch -c side-branch
fatal: a branch named 'side-branch' already exists
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git add history.txt                                      
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro>  git commit -m "Side branch commit"
[feature/lab2 3a90fce] Side branch commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 history.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git switch -
Switched to branch 'side-branch'
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git log --oneline --graph --all
* 3a90fce (feature/lab2) Side branch commit
* 69978c0 (HEAD -> side-branch, origin/feature/lab2) Task 2 done
| * b976f95 (git-reset-practice) Third commit
| * 28539c2 Second commit
| * 793869d First commit
|/
* 244b41e Task 1 complete
* 7584bed (main) Add test file
| *   63e0daf (origin/main, origin/HEAD) Merge branch 'inno-devops-labs:main' into main
| |\
| |/
|/|
* | 6f044dd (upstream/main) Replace IPFS with Nix
* | 0a87e1c refactor: reduce prescriptiveness in GitLab CI instructions
* | eaea715 feat: add GitLab CI alternative instructions to lab3
| * 4515622 chore: add PR template
|/
| * 0d2540f (origin/feature/lab1, feature/lab1) docs: Finished submissions.md (surly this time)
| * 9b1a595 docs: Finished submissions.md
| * 3995b9d docs: Added .png file with my SSH key on github
| * fb05349 docs: Added .png file with autofilled template for PR
| * 098f2a6 docs: Added .png file with my verified commit in github
```
I created a short-lived branch (`side-branch`), added one commit, switched back to the previous branch, and ran:

`git log --oneline --graph --all`

The graph output is shown above. It displays the side branch as a separate line, which makes branch structure easy to read.

Commit messages used in this task:
Side branch commit


Reflection:
The graph view helps me quickly understand where commits were made and how branches diverge.  
It is much easier to track history in team work than reading a flat log.

**Task 4:**
I created a lightweight tag on the latest commit:

`git tag v1.0.0`  
`git push origin v1.0.0`

Associated hash for `v1.0.0`: `f8aa16a3377f355d6728292b50135d733903876c`  
(checked with `git rev-list -n 1 v1.0.0`)

Why tags matter:
Tags mark important points in history, like release versions.  
They make it easy to find stable states, connect CI/CD to releases, and prepare release notes.

**Task 5:**
```
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git switch cmd-compare   
Switched to branch 'cmd-compare'
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> echo "scratch" >> demo.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git add demo.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git commit -m "chore: add demo file for restore test"
[cmd-compare fc58990] chore: add demo file for restore test
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 demo.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> echo "working" >> demo.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git status
On branch cmd-compare
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   demo.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git restore demo.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git status
On branch cmd-compare
nothing to commit, working tree clean
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> echo "staged change" >> demo.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git add demo.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git status
On branch cmd-compare
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   demo.txt

PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git restore --staged demo.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git status
On branch cmd-compare
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   demo.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> echo "v2 change" >> demo.txt    
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git add demo.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git commit -m "chore: update demo file"
[cmd-compare db5f8db] chore: update demo file
 1 file changed, 0 insertions(+), 0 deletions(-)
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> 
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git restore --source=HEAD~1 demo.txt
PS C:\Users\Roman\Documents\GitCourse\DevOps-Intro> git status
On branch cmd-compare
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   demo.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

### When to use commands:

Use `git switch` for branch operations.  
Use `git restore` for file state changes.  
Use `git checkout` mainly for older workflows or compatibility.


**Task 6:**
## GitHub Community

I starred the course repository and the simple-container-com/api project, and followed the professor, TAs, and classmates.  
Starring helps discover and bookmark useful open-source projects, while following developers helps me learn from their activity and improve collaboration in team projects.
