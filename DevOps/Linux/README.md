# Git
- [Soft Link vs Hard Link](#soft_link_vs_hard_link)
- [git stash](#git_stash)

## Soft Link vs Hard Link <a name="soft_link_vs_hard_link"></a>
- Soft Link - Soft link, also known as a symbolic link, is a special sort of file that points at a different file. You could think of it like a Windows shortcut. Soft links can point at entire directories or link to files on remote computers.
- Hard Link - It is a reference to address in memory. It works similarly to Python variable reference. Even if you delete an original file the hard link file will still have a reference to this file so the file it is still in drive memory. Hard links can only reference a file (not to directories or files on remote computers). Make changes in one of the file (original or hard link) will be reflected in both.