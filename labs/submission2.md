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
